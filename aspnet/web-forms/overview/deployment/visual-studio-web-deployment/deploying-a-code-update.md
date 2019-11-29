---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update
title: 使用 Visual Studio 的 ASP.NET Web 部署：部署代码更新 |Microsoft Docs
author: tdykstra
description: 本系列教程介绍了如何通过来将 ASP.NET web 应用程序部署（发布）到 Azure App Service Web 应用或第三方托管提供程序。
ms.author: riande
ms.date: 02/15/2013
ms.assetid: c76dbc35-a914-4ee3-919c-4f4d1fa05104
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update
msc.type: authoredcontent
ms.openlocfilehash: 3881833bfe2a50a38a357614f92f434a04a8ab08
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74626782"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-a-code-update"></a><span data-ttu-id="9794c-103">使用 Visual Studio 的 ASP.NET Web 部署：部署代码更新</span><span class="sxs-lookup"><span data-stu-id="9794c-103">ASP.NET Web Deployment using Visual Studio: Deploying a Code Update</span></span>

<span data-ttu-id="9794c-104">作者： [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="9794c-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="9794c-105">下载初学者项目</span><span class="sxs-lookup"><span data-stu-id="9794c-105">Download Starter Project</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="9794c-106">本系列教程介绍了如何使用 Visual Studio 2012 或 Visual Studio 2010，将 ASP.NET web 应用程序部署（发布）到 Azure App Service Web 应用或第三方托管提供商。</span><span class="sxs-lookup"><span data-stu-id="9794c-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="9794c-107">有关序列的信息，请参阅本[系列中的第一个教程](introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="9794c-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="9794c-108">概述</span><span class="sxs-lookup"><span data-stu-id="9794c-108">Overview</span></span>

<span data-ttu-id="9794c-109">初始部署完成后，你维护和开发网站的工作将继续进行，在此之前，你将需要部署更新。</span><span class="sxs-lookup"><span data-stu-id="9794c-109">After the initial deployment, your work of maintaining and developing your web site continues, and before long you will want to deploy an update.</span></span> <span data-ttu-id="9794c-110">本教程将指导你完成将更新部署到应用程序代码的过程。</span><span class="sxs-lookup"><span data-stu-id="9794c-110">This tutorial takes you through the process of deploying an update to your application code.</span></span> <span data-ttu-id="9794c-111">在本教程中实现和部署的更新不涉及数据库更改;在下一教程中，你将看到有关部署数据库更改的不同之处。</span><span class="sxs-lookup"><span data-stu-id="9794c-111">The update that you implement and deploy in this tutorial does not involve a database change; you'll see what's different about deploying a database change in the next tutorial.</span></span>

<span data-ttu-id="9794c-112">提醒：如果你收到一条错误消息或在你完成本教程时无法正常工作，请务必查看[故障排除页](troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="9794c-112">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](troubleshooting.md).</span></span>

## <a name="make-a-code-change"></a><span data-ttu-id="9794c-113">更改代码</span><span class="sxs-lookup"><span data-stu-id="9794c-113">Make a code change</span></span>

<span data-ttu-id="9794c-114">作为应用程序更新的简单示例，你将向**讲师**页添加选定讲师讲授的课程列表。</span><span class="sxs-lookup"><span data-stu-id="9794c-114">As a simple example of an update to your application, you'll add to the **Instructors** page a list of courses taught by the selected instructor.</span></span>

<span data-ttu-id="9794c-115">如果您运行的是**讲师**页，您会注意到网格中有**选择**的链接，但除了使行背景变为灰色以外，它们不会执行任何操作。</span><span class="sxs-lookup"><span data-stu-id="9794c-115">If you run the **Instructors** page, you'll notice that there are **Select** links in the grid, but they don't do anything other than make the row background turn gray.</span></span>

![带有选择的指导员页面](deploying-a-code-update/_static/image1.png)

<span data-ttu-id="9794c-117">现在，你将添加在单击 "**选择**" 链接时运行的代码，并显示所选指导员讲授的课程列表。</span><span class="sxs-lookup"><span data-stu-id="9794c-117">Now you'll add code that runs when the **Select** link is clicked and displays a list of courses taught by the selected instructor .</span></span>

1. <span data-ttu-id="9794c-118">在*default.aspx*中，在**ErrorMessageLabel** `Label` 控件后立即添加以下标记：</span><span class="sxs-lookup"><span data-stu-id="9794c-118">In *Instructors.aspx*, add the following markup immediately after the **ErrorMessageLabel** `Label` control:</span></span>

    [!code-aspx[Main](deploying-a-code-update/samples/sample1.aspx)]
2. <span data-ttu-id="9794c-119">运行页面并选择一个指导员。</span><span class="sxs-lookup"><span data-stu-id="9794c-119">Run the page and select an instructor.</span></span> <span data-ttu-id="9794c-120">你将看到该教师讲授的课程列表。</span><span class="sxs-lookup"><span data-stu-id="9794c-120">You see a list of courses taught by that instructor.</span></span>

    ![讲授课程的教师页面](deploying-a-code-update/_static/image2.png)
3. <span data-ttu-id="9794c-122">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="9794c-122">Close the browser.</span></span>

## <a name="deploy-the-code-update-to-the-test-environment"></a><span data-ttu-id="9794c-123">将代码更新部署到测试环境</span><span class="sxs-lookup"><span data-stu-id="9794c-123">Deploy the code update to the test environment</span></span>

<span data-ttu-id="9794c-124">在可以使用您的发布配置文件部署到测试、过渡和生产环境之前，您需要更改数据库发布选项。</span><span class="sxs-lookup"><span data-stu-id="9794c-124">Before you can use your publish profiles to deploy to test, staging, and production, you need to change database publishing options.</span></span> <span data-ttu-id="9794c-125">不再需要为成员资格数据库运行 grant 和数据部署脚本。</span><span class="sxs-lookup"><span data-stu-id="9794c-125">You no longer need to run the grant and data deployment scripts for the membership database.</span></span>

1. <span data-ttu-id="9794c-126">右键单击 "ContosoUniversity" 项目并单击 "**发布**"，打开 "**发布 Web** " 向导。</span><span class="sxs-lookup"><span data-stu-id="9794c-126">Open the **Publish Web** wizard by right-clicking the ContosoUniversity project and clicking **Publish**.</span></span>
2. <span data-ttu-id="9794c-127">单击 "**配置文件**" 下拉列表中的**测试**配置文件。</span><span class="sxs-lookup"><span data-stu-id="9794c-127">Click the **Test** profile in the **Profile** drop-down list.</span></span>
3. <span data-ttu-id="9794c-128">单击 "**设置**" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="9794c-128">Click the **Settings** tab.</span></span>
4. <span data-ttu-id="9794c-129">在 "**数据库**" 部分的 " **DefaultConnection** " 下，清除 "**更新数据库**" 复选框。</span><span class="sxs-lookup"><span data-stu-id="9794c-129">Under **DefaultConnection** in the **Databases** section, clear the **Update database** check box.</span></span>
5. <span data-ttu-id="9794c-130">单击 "**配置文件**" 选项卡，然后单击 "**配置文件**" 下拉列表中的**临时**配置文件。</span><span class="sxs-lookup"><span data-stu-id="9794c-130">Click the **Profile** tab, and then click the **Staging** profile in the **Profile** drop-down list.</span></span>
6. <span data-ttu-id="9794c-131">当系统询问你是否要保存对**测试**配置文件所做的更改时，请单击 **"是"** 。</span><span class="sxs-lookup"><span data-stu-id="9794c-131">When you are asked if you want to save the changes made to the **Test** profile, click **Yes**.</span></span>
7. <span data-ttu-id="9794c-132">在临时配置文件中进行相同的更改。</span><span class="sxs-lookup"><span data-stu-id="9794c-132">Make the same change in the Staging profile.</span></span>
8. <span data-ttu-id="9794c-133">重复此过程以在生产配置文件中进行相同的更改。</span><span class="sxs-lookup"><span data-stu-id="9794c-133">Repeat the process to make the same change in the Production profile.</span></span>
9. <span data-ttu-id="9794c-134">关闭 "**发布 Web** " 向导。</span><span class="sxs-lookup"><span data-stu-id="9794c-134">Close the **Publish Web** wizard.</span></span>

<span data-ttu-id="9794c-135">现在，只需运行一次单击 "发布" 即可部署到测试环境。</span><span class="sxs-lookup"><span data-stu-id="9794c-135">Deploying to the test environment is now a simple matter of running one-click publish again.</span></span> <span data-ttu-id="9794c-136">若要使此过程更快，你可以使用**Web 一键式发布**工具栏。</span><span class="sxs-lookup"><span data-stu-id="9794c-136">To make this process quicker, you can use the **Web One Click Publish** toolbar.</span></span>

1. <span data-ttu-id="9794c-137">在 "**视图**" 菜单中选择 "**工具栏**"，然后选择 **"Web 一键式发布"** 。</span><span class="sxs-lookup"><span data-stu-id="9794c-137">In the **View** menu, choose **Toolbars** and then select **Web One Click Publish**.</span></span>

    ![Selecting_One_Click_Publish_toolbar](deploying-a-code-update/_static/image3.png)
2. <span data-ttu-id="9794c-139">在**解决方案资源管理器**中，选择 ContosoUniversity 项目。</span><span class="sxs-lookup"><span data-stu-id="9794c-139">In **Solution Explorer**, select the ContosoUniversity project.</span></span>
3. <span data-ttu-id="9794c-140">**Web 一键式发布**工具栏上，选择 "**测试**发布配置文件"，然后单击 "**发布 Web** " （其箭头指向左侧和右侧的图标）。</span><span class="sxs-lookup"><span data-stu-id="9794c-140">the **Web One Click Publish** toolbar, choose the **Test** publish profile and then click **Publish Web** (the icon with arrows pointing left and right).</span></span>

    ![Web_One_Click_Publish_toolbar](deploying-a-code-update/_static/image4.png)
4. <span data-ttu-id="9794c-142">Visual Studio 将部署更新后的应用程序，浏览器会自动打开到主页。</span><span class="sxs-lookup"><span data-stu-id="9794c-142">Visual Studio deploys the updated application, and the browser automatically opens to the home page.</span></span>
5. <span data-ttu-id="9794c-143">运行 "讲师" 页，然后选择一个教师来验证更新是否已成功部署。</span><span class="sxs-lookup"><span data-stu-id="9794c-143">Run the Instructors page and select an instructor to verify that the update was successfully deployed.</span></span>

<span data-ttu-id="9794c-144">通常情况下，还会进行回归测试（即，测试站点的其余部分以确保新的更改不会破坏现有的任何功能）。</span><span class="sxs-lookup"><span data-stu-id="9794c-144">You would normally also do regression testing (that is, test the rest of the site to make sure that the new change didn't break any existing functionality).</span></span> <span data-ttu-id="9794c-145">但对于本教程，你将跳过该步骤，并继续将更新部署到过渡和生产环境。</span><span class="sxs-lookup"><span data-stu-id="9794c-145">But for this tutorial you'll skip that step and proceed to deploy the update to staging and production.</span></span>

<span data-ttu-id="9794c-146">重新部署时，Web 部署会自动确定哪些文件已更改，并且仅将更改的文件复制到服务器。</span><span class="sxs-lookup"><span data-stu-id="9794c-146">When you redeploy, Web Deploy automatically determines which files have changed and only copies changed files to the server.</span></span> <span data-ttu-id="9794c-147">默认情况下，Web 部署使用文件上次更改的日期来确定哪些文件已更改。</span><span class="sxs-lookup"><span data-stu-id="9794c-147">By default, Web Deploy uses last-changed dates on files to determine which ones have changed.</span></span> <span data-ttu-id="9794c-148">某些源代码管理系统会更改文件日期，即使您不更改文件内容也是如此。</span><span class="sxs-lookup"><span data-stu-id="9794c-148">Some source control systems change file dates even when you don't change the file contents.</span></span> <span data-ttu-id="9794c-149">在这种情况下，你可能希望将 Web 部署配置为使用文件校验和来确定哪些文件已更改。</span><span class="sxs-lookup"><span data-stu-id="9794c-149">In that case, you might want to configure Web Deploy to use file checksums to determine which files have changed.</span></span> <span data-ttu-id="9794c-150">有关详细信息，请参阅 ASP.NET 部署常见问题解答中的[为什么我不更改所有文件就](https://msdn.microsoft.com/library/ee942158.aspx#use_checksum)会重新部署。</span><span class="sxs-lookup"><span data-stu-id="9794c-150">For more information, see [Why do all of my files get redeployed although I didn't change them?](https://msdn.microsoft.com/library/ee942158.aspx#use_checksum) in the ASP.NET Deployment FAQ.</span></span>

## <a name="take-the-application-offline-during-deployment"></a><span data-ttu-id="9794c-151">在部署过程中使应用程序脱机</span><span class="sxs-lookup"><span data-stu-id="9794c-151">Take the application offline during deployment</span></span>

<span data-ttu-id="9794c-152">现在正在部署的更改是单个页面的简单更改。</span><span class="sxs-lookup"><span data-stu-id="9794c-152">The change you're deploying now is a simple change to a single page.</span></span> <span data-ttu-id="9794c-153">但有时，你可以部署更大的更改，或者同时部署代码和数据库更改，如果用户在部署完成之前请求页面，则站点的行为可能会错误。</span><span class="sxs-lookup"><span data-stu-id="9794c-153">But sometimes you deploy larger changes, or you deploy both code and database changes, and the site might behave incorrectly if a user requests a page before deployment is finished.</span></span> <span data-ttu-id="9794c-154">若要防止用户在部署过程中访问网站，可以使用*应用\_脱机 .htm*文件。</span><span class="sxs-lookup"><span data-stu-id="9794c-154">To prevent users from accessing the site while deployment is in progress, you can use an *app\_offline.htm* file.</span></span> <span data-ttu-id="9794c-155">在应用程序的根文件夹中将名为 "app" 的文件\_为 " *offline* " 时，IIS 会自动显示该文件，而不是运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="9794c-155">When you put a file named *app\_offline.htm* in the root folder of your application, IIS automatically displays that file instead of running your application.</span></span> <span data-ttu-id="9794c-156">因此，若要在部署过程中阻止访问，请在根文件夹中将*应用\_为 offline* ，运行部署过程，然后在成功部署后删除*应用\_脱机 .htm。*</span><span class="sxs-lookup"><span data-stu-id="9794c-156">So to prevent access during deployment, you put *app\_offline.htm* in the root folder, run the deployment process, and then remove *app\_offline.htm* after successful deployment.</span></span>

<span data-ttu-id="9794c-157">可以将 Web 部署配置为在服务器上开始部署时将默认*应用程序\_脱机 .htm*文件，并在其完成后将其删除。</span><span class="sxs-lookup"><span data-stu-id="9794c-157">You can configure Web Deploy to automatically put a default *app\_offline.htm* file on the server when it starts deploying and remove it when it finishes.</span></span> <span data-ttu-id="9794c-158">为此，只需将以下 XML 元素添加到发布配置文件（.pubxml）文件中：</span><span class="sxs-lookup"><span data-stu-id="9794c-158">To do that all you have to do is add the following XML element to your publish profile (.pubxml) file:</span></span>

[!code-xml[Main](deploying-a-code-update/samples/sample2.xml)]

<span data-ttu-id="9794c-159">在本教程中，你将了解如何创建和使用自定义*应用\_脱机 .htm*文件。</span><span class="sxs-lookup"><span data-stu-id="9794c-159">For this tutorial you'll see how to create and use a custom *app\_offline.htm* file.</span></span>

<span data-ttu-id="9794c-160">不需要在暂存站点中使用*应用\_.htm* ，因为你没有访问过渡站点的用户。</span><span class="sxs-lookup"><span data-stu-id="9794c-160">Using *app\_offline.htm* in the staging site isn't required, because you don't have users accessing the staging site.</span></span> <span data-ttu-id="9794c-161">但使用过渡测试计划在生产中部署的方式是一种很好的做法。</span><span class="sxs-lookup"><span data-stu-id="9794c-161">But it's a good practice to use staging to test everything the way you plan to deploy in production.</span></span>

### <a name="create-app_offlinehtm"></a><span data-ttu-id="9794c-162">创建脱机应用\_</span><span class="sxs-lookup"><span data-stu-id="9794c-162">Create app\_offline.htm</span></span>

1. <span data-ttu-id="9794c-163">在**解决方案资源管理器**中，右键单击解决方案并单击 "**添加**"，然后单击 "**新建项**"。</span><span class="sxs-lookup"><span data-stu-id="9794c-163">In **Solution Explorer**, right-click the solution and click **Add**, and then click **New Item**.</span></span>
2. <span data-ttu-id="9794c-164">创建一个名为 " *app\_* " 的**HTML 页面**（在默认情况下，Visual Studio 创建的 *.html*扩展中删除最终的 "l"）。</span><span class="sxs-lookup"><span data-stu-id="9794c-164">Create an **HTML Page** named *app\_offline.htm* (delete the final "l" in the *.html* extension that Visual Studio creates by default).</span></span>
3. <span data-ttu-id="9794c-165">将模板标记替换为以下标记：</span><span class="sxs-lookup"><span data-stu-id="9794c-165">Replace the template markup with the following markup:</span></span>

    [!code-html[Main](deploying-a-code-update/samples/sample3.html)]
4. <span data-ttu-id="9794c-166">保存并关闭文件。</span><span class="sxs-lookup"><span data-stu-id="9794c-166">Save and close the file.</span></span>

### <a name="copy-app_offlinehtm-to-the-root-folder-of-the-web-site"></a><span data-ttu-id="9794c-167">将应用\_脱机复制到网站的根文件夹</span><span class="sxs-lookup"><span data-stu-id="9794c-167">Copy app\_offline.htm to the root folder of the web site</span></span>

<span data-ttu-id="9794c-168">您可以使用任何 FTP 工具将文件复制到网站。</span><span class="sxs-lookup"><span data-stu-id="9794c-168">You can use any FTP tool to copy files to the web site.</span></span> <span data-ttu-id="9794c-169">[FileZilla](http://filezilla-project.org/)是一种常用的 FTP 工具，在屏幕截图中显示。</span><span class="sxs-lookup"><span data-stu-id="9794c-169">[FileZilla](http://filezilla-project.org/) is a popular FTP tool and is shown in the screen shots.</span></span>

<span data-ttu-id="9794c-170">若要使用 FTP 工具，需要执行以下三项操作： FTP URL、用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="9794c-170">To use an FTP tool, you need three things: the FTP URL, the user name, and the password.</span></span>

<span data-ttu-id="9794c-171">URL 显示在 Azure 管理门户中网站的 "仪表板" 页上，可以在前面下载的 *.publishsettings*文件中找到 FTP 的用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="9794c-171">The URL is shown on the web site's dashboard page in the Azure Management Portal, and the user name and password for FTP can be found in the *.publishsettings* file that you downloaded earlier.</span></span> <span data-ttu-id="9794c-172">以下步骤演示如何获取这些值。</span><span class="sxs-lookup"><span data-stu-id="9794c-172">The following steps show how to get these values.</span></span>

1. <span data-ttu-id="9794c-173">在 Azure 管理门户中，单击 **"网站" 选项卡**，然后单击 "暂存" 网站。</span><span class="sxs-lookup"><span data-stu-id="9794c-173">In the Azure Management Portal, click **Web Sites** tab and then click the staging web site.</span></span>
2. <span data-ttu-id="9794c-174">在 "**仪表板**" 页上，向下滚动到 "**速览**" 部分中的 "FTP 主机名"。</span><span class="sxs-lookup"><span data-stu-id="9794c-174">On the **Dashboard** page, scroll down to find the FTP host name in the **Quick Glance** section.</span></span>

    ![FTP 主机名](deploying-a-code-update/_static/image5.png)
3. <span data-ttu-id="9794c-176">在记事本或其他文本编辑器中打开 *.publishsettings*文件。</span><span class="sxs-lookup"><span data-stu-id="9794c-176">Open the staging *.publishsettings* file in Notepad or another text editor.</span></span>
4. <span data-ttu-id="9794c-177">找到 FTP 配置文件的 `publishProfile` 元素。</span><span class="sxs-lookup"><span data-stu-id="9794c-177">Find the `publishProfile` element for the FTP profile.</span></span>
5. <span data-ttu-id="9794c-178">复制 `userName` 和 `userPWD` 值。</span><span class="sxs-lookup"><span data-stu-id="9794c-178">Copy the `userName` and `userPWD` values.</span></span>

    ![FTP 凭据](deploying-a-code-update/_static/image6.png)
6. <span data-ttu-id="9794c-180">打开 FTP 工具并登录到 FTP URL。</span><span class="sxs-lookup"><span data-stu-id="9794c-180">Open your FTP tool and log on to the FTP URL.</span></span>
7. <span data-ttu-id="9794c-181">将*应用\_.htm*从解决方案文件夹复制到临时站点中的 */site/wwwroot*文件夹。</span><span class="sxs-lookup"><span data-stu-id="9794c-181">Copy *app\_offline.htm* from the solution folder to the */site/wwwroot* folder in the staging site.</span></span>

    ![复制 app_offline](deploying-a-code-update/_static/image7.png)
8. <span data-ttu-id="9794c-183">浏览到过渡站点的 URL。</span><span class="sxs-lookup"><span data-stu-id="9794c-183">Browse to your staging site's URL.</span></span> <span data-ttu-id="9794c-184">此时将显示 "*应用\_offline* " 页，而不是主页。</span><span class="sxs-lookup"><span data-stu-id="9794c-184">You see that the *app\_offline.htm* page is now displayed instead of your home page.</span></span>

    ![在浏览器窗口中 app_offline .htm](deploying-a-code-update/_static/image8.png)

<span data-ttu-id="9794c-186">你现在已准备好部署到过渡环境。</span><span class="sxs-lookup"><span data-stu-id="9794c-186">You are now ready to deploy to staging.</span></span>

## <a name="deploy-the-code-update-to-staging-and-production"></a><span data-ttu-id="9794c-187">将代码更新部署到过渡和生产环境</span><span class="sxs-lookup"><span data-stu-id="9794c-187">Deploy the code update to staging and production</span></span>

1. <span data-ttu-id="9794c-188">在**Web 一键式发布**工具栏中，选择**过渡**发布配置文件，然后单击 "**发布 Web**"。</span><span class="sxs-lookup"><span data-stu-id="9794c-188">In the **Web One Click Publish** toolbar, choose the **Staging** publish profile and then click **Publish Web**.</span></span>

    <span data-ttu-id="9794c-189">Visual Studio 将部署更新后的应用程序，并将浏览器打开到站点的主页。</span><span class="sxs-lookup"><span data-stu-id="9794c-189">Visual Studio deploys the updated application and opens the browser to the site's home page.</span></span> <span data-ttu-id="9794c-190">将显示*应用程序\_脱机 .htm*文件。</span><span class="sxs-lookup"><span data-stu-id="9794c-190">The *app\_offline.htm* file is displayed.</span></span> <span data-ttu-id="9794c-191">必须先删除*应用\_脱机 .htm*文件，然后才能进行测试以验证部署是否成功。</span><span class="sxs-lookup"><span data-stu-id="9794c-191">Before you can test to verify successful deployment, you must remove the *app\_offline.htm* file.</span></span>
2. <span data-ttu-id="9794c-192">返回到 FTP 工具，并从临时站点删除**应用\_offline。**</span><span class="sxs-lookup"><span data-stu-id="9794c-192">Return to your FTP tool, and delete **app\_offline.htm** from the staging site.</span></span>
3. <span data-ttu-id="9794c-193">在浏览器中，打开过渡站点中的 "讲师" 页，然后选择一个教师来验证更新是否已成功部署。</span><span class="sxs-lookup"><span data-stu-id="9794c-193">In the browser, open the Instructors page in the staging site, and select an instructor to verify that the update was successfully deployed.</span></span>
4. <span data-ttu-id="9794c-194">对于生产，请遵循与进行过渡时相同的过程。</span><span class="sxs-lookup"><span data-stu-id="9794c-194">Follow the same procedure for production as you did for staging.</span></span>

<a id="specificfiles"></a>

## <a name="reviewing-changes-and-deploying-specific-files"></a><span data-ttu-id="9794c-195">查看更改并部署特定文件</span><span class="sxs-lookup"><span data-stu-id="9794c-195">Reviewing Changes and Deploying Specific Files</span></span>

<span data-ttu-id="9794c-196">Visual Studio 2012 还提供了部署单个文件的能力。</span><span class="sxs-lookup"><span data-stu-id="9794c-196">Visual Studio 2012 also gives you the ability to deploy individual files.</span></span> <span data-ttu-id="9794c-197">对于选定的文件，您可以查看本地版本和已部署的版本之间的差异，将文件部署到目标环境，或将文件从目标环境复制到本地项目中。</span><span class="sxs-lookup"><span data-stu-id="9794c-197">For a selected file you can view differences between the local version and the deployed version, deploy the file to the destination environment, or copy the file from the destination environment to the local project.</span></span> <span data-ttu-id="9794c-198">在本教程的此部分中，你将了解如何使用这些功能。</span><span class="sxs-lookup"><span data-stu-id="9794c-198">In this section of the tutorial you see how to use these features.</span></span>

### <a name="make-a-change-to-deploy"></a><span data-ttu-id="9794c-199">进行部署更改</span><span class="sxs-lookup"><span data-stu-id="9794c-199">Make a change to deploy</span></span>

1. <span data-ttu-id="9794c-200">打开*Content/站点导航*，查找 `body` 标记的块。</span><span class="sxs-lookup"><span data-stu-id="9794c-200">Open *Content/Site.css*, and find the block for the `body` tag.</span></span>
2. <span data-ttu-id="9794c-201">将 `background-color` 的值从 "`#fff`" 更改为 "`darkblue`"。</span><span class="sxs-lookup"><span data-stu-id="9794c-201">Change the value for `background-color` from `#fff` to `darkblue`.</span></span>

    [!code-css[Main](deploying-a-code-update/samples/sample4.css?highlight=2)]

### <a name="view-the-change-in-the-publish-preview-window"></a><span data-ttu-id="9794c-202">在发布预览窗口中查看更改</span><span class="sxs-lookup"><span data-stu-id="9794c-202">View the change in the Publish Preview window</span></span>

<span data-ttu-id="9794c-203">使用 "**发布 Web** " 向导发布项目时，可以通过在**预览**窗口中双击文件来查看要发布的更改。</span><span class="sxs-lookup"><span data-stu-id="9794c-203">When you use the **Publish Web** wizard to publish the project, you can see what changes are going to be published by double-clicking the file in the **Preview** window.</span></span>

1. <span data-ttu-id="9794c-204">右键单击 "ContosoUniversity" 项目，然后单击 "**发布**"。</span><span class="sxs-lookup"><span data-stu-id="9794c-204">Right-click the ContosoUniversity project and click **Publish**.</span></span>
2. <span data-ttu-id="9794c-205">从 "**配置文件**" 下拉列表中，选择 "**测试**发布配置文件"。</span><span class="sxs-lookup"><span data-stu-id="9794c-205">From the **Profile** drop-down list, select the **Test** publish profile.</span></span>
3. <span data-ttu-id="9794c-206">单击 "**预览**"，然后单击 "**开始预览**"。</span><span class="sxs-lookup"><span data-stu-id="9794c-206">Click **Preview**, and then click **Start Preview**.</span></span>
4. <span data-ttu-id="9794c-207">在**预览**窗格中，双击 **"web.config"。**</span><span class="sxs-lookup"><span data-stu-id="9794c-207">In the **Preview** pane, double-click **Site.css**.</span></span>

    ![双击 "网站地图"](deploying-a-code-update/_static/image9.png)

    <span data-ttu-id="9794c-209">"**预览更改**" 对话框显示将要部署的更改的预览。</span><span class="sxs-lookup"><span data-stu-id="9794c-209">The **Preview changes** dialog shows a preview of the changes that will be deployed.</span></span>

    ![预览对站点的更改](deploying-a-code-update/_static/image10.png)

    <span data-ttu-id="9794c-211">如果双击*web.config 文件，* 则 "**预览更改**" 对话框将显示生成配置转换和发布配置文件转换的效果。</span><span class="sxs-lookup"><span data-stu-id="9794c-211">If you double-click the *Web.config* file, the **Preview changes** dialog shows the effect of your build configuration transformations and publish profile transformations.</span></span> <span data-ttu-id="9794c-212">此时，你未执行任何操作来导致服务器上的*web.config 文件发生*更改，因此你不会看到任何更改。</span><span class="sxs-lookup"><span data-stu-id="9794c-212">At this point you have not done anything that would cause the *Web.config* file on the server to change, so you expect to see no changes.</span></span> <span data-ttu-id="9794c-213">但是，"**预览更改**" 窗口错误地显示两个更改。</span><span class="sxs-lookup"><span data-stu-id="9794c-213">However, the **Preview changes** window incorrectly shows two changes.</span></span> <span data-ttu-id="9794c-214">将删除两个 XML 元素。</span><span class="sxs-lookup"><span data-stu-id="9794c-214">It looks like two XML elements will be removed.</span></span> <span data-ttu-id="9794c-215">当你在 Code First 上下文类的**应用程序启动上选择 "执行 Code First 迁移**时，发布过程将添加这些元素。</span><span class="sxs-lookup"><span data-stu-id="9794c-215">These elements are added by the publish process when you select **Execute Code First Migrations on application start** for a Code First context class.</span></span> <span data-ttu-id="9794c-216">比较是在发布过程添加这些元素之前完成的，因此，它看起来像是要删除它们，不过它们将不会被删除。</span><span class="sxs-lookup"><span data-stu-id="9794c-216">The comparison is done before the publish process adds those elements, so it looks like they are being removed although they will not be removed.</span></span> <span data-ttu-id="9794c-217">此错误将在将来的版本中得到更正。</span><span class="sxs-lookup"><span data-stu-id="9794c-217">This error will be corrected in a future release.</span></span>
5. <span data-ttu-id="9794c-218">单击 **“关闭”** 。</span><span class="sxs-lookup"><span data-stu-id="9794c-218">Click **Close**.</span></span>
6. <span data-ttu-id="9794c-219">单击“发布”。</span><span class="sxs-lookup"><span data-stu-id="9794c-219">Click **Publish**.</span></span>
7. <span data-ttu-id="9794c-220">当浏览器打开到测试网站的主页时，按 CTRL + F5 以引发硬刷新，以便查看 CSS 更改的效果。</span><span class="sxs-lookup"><span data-stu-id="9794c-220">When the browser opens to the home page of the Test site, press CTRL+F5 to cause a hard refresh in order to see the effect of the CSS change.</span></span>

    ![CSS 更改的效果](deploying-a-code-update/_static/image11.png)
8. <span data-ttu-id="9794c-222">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="9794c-222">Close the browser.</span></span>

### <a name="publish-specific-files-from-solution-explorer"></a><span data-ttu-id="9794c-223">从解决方案资源管理器发布特定文件</span><span class="sxs-lookup"><span data-stu-id="9794c-223">Publish specific files from Solution Explorer</span></span>

<span data-ttu-id="9794c-224">假设您不喜欢蓝色背景并且要恢复为原始颜色。</span><span class="sxs-lookup"><span data-stu-id="9794c-224">Suppose you don't like the blue background and want to revert to the original color.</span></span> <span data-ttu-id="9794c-225">在本部分中，你将通过直接从**解决方案资源管理器**发布特定文件来还原原始设置。</span><span class="sxs-lookup"><span data-stu-id="9794c-225">In this section you'll restore the original settings by publishing a specific file directly from **Solution Explorer**.</span></span>

1. <span data-ttu-id="9794c-226">打开*Content/Site .css*并将 `background-color` 设置还原为 `#fff`。</span><span class="sxs-lookup"><span data-stu-id="9794c-226">Open *Content/Site.css* and restore the `background-color` setting to `#fff`.</span></span>
2. <span data-ttu-id="9794c-227">在**解决方案资源管理器**中，右键单击*Content/Site .css*文件。</span><span class="sxs-lookup"><span data-stu-id="9794c-227">In **Solution Explorer**, right-click the *Content/Site.css* file.</span></span>

    <span data-ttu-id="9794c-228">上下文菜单显示了三个发布选项。</span><span class="sxs-lookup"><span data-stu-id="9794c-228">The context menu shows three publish options.</span></span>

    ![从解决方案资源管理器发布选项](deploying-a-code-update/_static/image12.png)
3. <span data-ttu-id="9794c-230">单击 "**预览对站点的更改**"。</span><span class="sxs-lookup"><span data-stu-id="9794c-230">Click **Preview changes to Site.css**.</span></span>

    <span data-ttu-id="9794c-231">此时会打开一个窗口，以显示本地文件与目标环境中的本地文件版本之间的差异。</span><span class="sxs-lookup"><span data-stu-id="9794c-231">A window opens to show the differences between the local file and the version of it in the destination environment.</span></span>

    ![Diff-Content/站点导航](deploying-a-code-update/_static/image13.png)
4. <span data-ttu-id="9794c-233">在**解决方案资源管理器**中，再次右键单击 "**网站**"，然后单击 "**发布网站**"。</span><span class="sxs-lookup"><span data-stu-id="9794c-233">In **Solution Explorer**, right-click **Site.css** again and click **Publish Site.css**.</span></span>

    <span data-ttu-id="9794c-234">" **Web 发布活动**" 窗口显示该文件已发布。</span><span class="sxs-lookup"><span data-stu-id="9794c-234">The **Web Publish Activity** window shows that the file has been published.</span></span>

    !["Web 发布活动" 窗口](deploying-a-code-update/_static/image14.png)
5. <span data-ttu-id="9794c-236">在浏览器中打开 `http://localhost/contosouniversity` URL，然后按 CTRL + F5 以引发硬刷新，以便查看 CSS 更改的效果。</span><span class="sxs-lookup"><span data-stu-id="9794c-236">Open a browser to the `http://localhost/contosouniversity` URL, and then press CTRL+F5 to cause a hard refresh in order to see the effect of the CSS change.</span></span>

    ![包含普通 CSS 的主页](deploying-a-code-update/_static/image15.png)
6. <span data-ttu-id="9794c-238">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="9794c-238">Close the browser.</span></span>

## <a name="summary"></a><span data-ttu-id="9794c-239">总结</span><span class="sxs-lookup"><span data-stu-id="9794c-239">Summary</span></span>

<span data-ttu-id="9794c-240">现在，您已看到了几种部署不涉及数据库更改的应用程序更新的方法，并且您已了解如何预览更改以验证将更新的内容。</span><span class="sxs-lookup"><span data-stu-id="9794c-240">You've now seen several ways to deploy an application update that does not involve a database change, and you've seen how to preview the changes to verify that what will be updated is what you expect.</span></span> <span data-ttu-id="9794c-241">讲师页现在提供了一个**课程讲授**部分。</span><span class="sxs-lookup"><span data-stu-id="9794c-241">The Instructors page now has a **Courses Taught** section.</span></span>

![讲授课程的教师页面](deploying-a-code-update/_static/image16.png)

<span data-ttu-id="9794c-243">下一教程将演示如何部署数据库更改：将 "生日" 字段添加到数据库和 "讲师" 页。</span><span class="sxs-lookup"><span data-stu-id="9794c-243">The next tutorial shows you how to deploy a database change: you'll add a birthdate field to the database and to the Instructors page.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9794c-244">[上一页](deploying-to-production.md)
> [下一页](deploying-a-database-update.md)</span><span class="sxs-lookup"><span data-stu-id="9794c-244">[Previous](deploying-to-production.md)
[Next](deploying-a-database-update.md)</span></span>
