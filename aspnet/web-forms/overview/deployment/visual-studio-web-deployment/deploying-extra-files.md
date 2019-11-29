---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files
title: 使用 Visual Studio 的 ASP.NET Web 部署：部署额外文件 |Microsoft Docs
author: tdykstra
description: 本系列教程介绍了如何通过来将 ASP.NET web 应用程序部署（发布）到 Azure App Service Web 应用或第三方托管提供程序。
ms.author: riande
ms.date: 03/23/2015
ms.assetid: 1cd91055-84bc-42c6-9d80-646f41429d4d
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files
msc.type: authoredcontent
ms.openlocfilehash: eaa3141c22980f0c816e2f33b5597ac9fe69c23c
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74594896"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-extra-files"></a><span data-ttu-id="1be40-103">使用 Visual Studio 的 ASP.NET Web 部署：部署额外文件</span><span class="sxs-lookup"><span data-stu-id="1be40-103">ASP.NET Web Deployment using Visual Studio: Deploying Extra Files</span></span>

<span data-ttu-id="1be40-104">作者： [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="1be40-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="1be40-105">下载初学者项目</span><span class="sxs-lookup"><span data-stu-id="1be40-105">Download Starter Project</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="1be40-106">本系列教程介绍了如何使用 Visual Studio 2012 或 Visual Studio 2010，将 ASP.NET web 应用程序部署（发布）到 Azure App Service Web 应用或第三方托管提供商。</span><span class="sxs-lookup"><span data-stu-id="1be40-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="1be40-107">有关序列的信息，请参阅本[系列中的第一个教程](introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="1be40-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="1be40-108">概述</span><span class="sxs-lookup"><span data-stu-id="1be40-108">Overview</span></span>

<span data-ttu-id="1be40-109">本教程介绍如何扩展 Visual Studio web 发布管道，以便在部署期间执行其他任务。</span><span class="sxs-lookup"><span data-stu-id="1be40-109">This tutorial shows how to extend the Visual Studio web publish pipeline to do an additional task during deployment.</span></span> <span data-ttu-id="1be40-110">任务是将不在项目文件夹中的多余文件复制到目标网站。</span><span class="sxs-lookup"><span data-stu-id="1be40-110">The task is to copy extra files that are not in the project folder to the destination web site.</span></span>

<span data-ttu-id="1be40-111">对于本教程，你将复制一个额外的文件：*机器人。*</span><span class="sxs-lookup"><span data-stu-id="1be40-111">For this tutorial you'll copy one extra file: *robots.txt*.</span></span> <span data-ttu-id="1be40-112">你希望将此文件部署到过渡，但不部署到生产环境。</span><span class="sxs-lookup"><span data-stu-id="1be40-112">You want to deploy this file to staging but not to production.</span></span> <span data-ttu-id="1be40-113">在[部署到生产](deploying-to-production.md)教程中，你已将此文件添加到项目中，并已将生产发布配置文件配置为排除它。</span><span class="sxs-lookup"><span data-stu-id="1be40-113">In [the Deploying to Production](deploying-to-production.md) tutorial, you added this file to the project and configured the Production publish profile to exclude it.</span></span> <span data-ttu-id="1be40-114">在本教程中，你将看到用于处理这种情况的一种替代方法，一种方法可用于要部署但不想包含在项目中的任何文件。</span><span class="sxs-lookup"><span data-stu-id="1be40-114">In this tutorial you'll see an alternative method to handle this situation, one that will be useful for any files that you want to deploy but don't want to include in the project.</span></span>

## <a name="move-the-robotstxt-file"></a><span data-ttu-id="1be40-115">移动机器人 .txt 文件</span><span class="sxs-lookup"><span data-stu-id="1be40-115">Move the robots.txt file</span></span>

<span data-ttu-id="1be40-116">若要为*机器人 .txt*提供不同的处理方法，请在本教程的本部分中，将该文件移动到项目中未包含的文件夹，并从过渡环境中删除*机器人。*</span><span class="sxs-lookup"><span data-stu-id="1be40-116">To prepare for a different method of handling *robots.txt*, in this section of the tutorial you move the file to a folder that is not included in the project, and you delete *robots.txt* from the staging environment.</span></span> <span data-ttu-id="1be40-117">需要从暂存中删除该文件，以便可以验证将该文件部署到该环境的新方法是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="1be40-117">It is necessary to delete the file from staging so that you can verify that your new method of deploying the file to that environment is working correctly.</span></span>

1. <span data-ttu-id="1be40-118">在**解决方案资源管理器**中，右键单击*机器人 .txt*文件，然后单击 "**从项目中排除**"。</span><span class="sxs-lookup"><span data-stu-id="1be40-118">In **Solution Explorer**, right-click the *robots.txt* file and click **Exclude From Project**.</span></span>
2. <span data-ttu-id="1be40-119">使用 Windows 文件资源管理器在解决方案文件夹中创建一个新文件夹，并将其命名为*ExtraFiles*。</span><span class="sxs-lookup"><span data-stu-id="1be40-119">Using Windows File Explorer, create a new folder in the solution folder and name it *ExtraFiles*.</span></span>
3. <span data-ttu-id="1be40-120">将*机器人 .txt*文件从*ContosoUniversity*项目文件夹移动到*ExtraFiles*文件夹。</span><span class="sxs-lookup"><span data-stu-id="1be40-120">Move the *robots.txt* file from the *ContosoUniversity* project folder to the *ExtraFiles* folder.</span></span>

    ![ExtraFiles 文件夹](deploying-extra-files/_static/image1.png)
4. <span data-ttu-id="1be40-122">使用 FTP 工具，从暂存网站中删除*机器人 .txt*文件。</span><span class="sxs-lookup"><span data-stu-id="1be40-122">Using your FTP tool, delete the *robots.txt* file from the staging web site.</span></span>

    <span data-ttu-id="1be40-123">作为替代方法，你可以在过渡发布配置文件的 "**设置**" 选项卡上的 "**文件发布选项**" 下选择 "**删除目标上的其他文件**"，然后重新发布到 "过渡"。</span><span class="sxs-lookup"><span data-stu-id="1be40-123">As an alternative, you can select **Remove additional files at destination** under **File Publish Options** on the **Settings** tab of the Staging publish profile, and republish to staging.</span></span>

## <a name="update-the-publish-profile-file"></a><span data-ttu-id="1be40-124">更新发布配置文件</span><span class="sxs-lookup"><span data-stu-id="1be40-124">Update the publish profile file</span></span>

<span data-ttu-id="1be40-125">仅在暂存中需要*机器人 .txt* ，因此，要进行部署，只需暂存需要更新的发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="1be40-125">You only need *robots.txt* in staging, so the only publish profile you need to update in order to deploy it is Staging.</span></span>

1. <span data-ttu-id="1be40-126">在 Visual Studio 中，打开 " *.pubxml*"。</span><span class="sxs-lookup"><span data-stu-id="1be40-126">In Visual Studio, open *Staging.pubxml*.</span></span>
2. <span data-ttu-id="1be40-127">在文件末尾的结束 `</Project>` 标记之前，添加以下标记：</span><span class="sxs-lookup"><span data-stu-id="1be40-127">At the end of the file, before the closing `</Project>` tag, add the following markup:</span></span>

    [!code-xml[Main](deploying-extra-files/samples/sample1.xml)]

    <span data-ttu-id="1be40-128">此代码将创建一个新的目标，该*目标*将收集其他要部署的文件。</span><span class="sxs-lookup"><span data-stu-id="1be40-128">This code creates a new *target* that will collect additional files to be deployed.</span></span> <span data-ttu-id="1be40-129">目标由一项或多项任务组成，MSBuild 将根据你指定的条件执行该任务。</span><span class="sxs-lookup"><span data-stu-id="1be40-129">A target is composed of one or more tasks that MSBuild will execute based on conditions you specify.</span></span>

    <span data-ttu-id="1be40-130">`Include` 特性指定要在其中查找文件的文件夹是*ExtraFiles*，位于与项目文件夹相同的级别。</span><span class="sxs-lookup"><span data-stu-id="1be40-130">The `Include` attribute specifies that the folder in which to find the files is *ExtraFiles*, located at the same level as the project folder.</span></span> <span data-ttu-id="1be40-131">MSBuild 将从该文件夹收集所有文件，并以递归方式从任何子文件夹中（双星号指定递归子文件夹）。</span><span class="sxs-lookup"><span data-stu-id="1be40-131">MSBuild will collect all files from that folder and recursively from any subfolders (the double asterisk specifies recursive subfolders).</span></span> <span data-ttu-id="1be40-132">利用此代码，你可以将多个文件和文件放在*ExtraFiles*文件夹内的子文件夹中，所有文件都将被部署。</span><span class="sxs-lookup"><span data-stu-id="1be40-132">With this code you could put multiple files, and files in subfolders inside the *ExtraFiles* folder, and all will be deployed.</span></span>

    <span data-ttu-id="1be40-133">`DestinationRelativePath` 元素指定应将文件夹和文件复制到目标网站的根文件夹中，与在*ExtraFiles*文件夹中找到的文件和文件夹结构相同。</span><span class="sxs-lookup"><span data-stu-id="1be40-133">The `DestinationRelativePath` element specifies that the folders and files should be copied to the root folder of the destination web site, in the same file and folder structure as they are found in the *ExtraFiles* folder.</span></span> <span data-ttu-id="1be40-134">如果要复制*ExtraFiles*文件夹本身，`DestinationRelativePath` 值将是*ExtraFiles\%（RecursiveDir）% （Filename）% （Extension）* 。</span><span class="sxs-lookup"><span data-stu-id="1be40-134">If you wanted to copy the *ExtraFiles* folder itself, the `DestinationRelativePath` value would be *ExtraFiles\%(RecursiveDir)%(Filename)%(Extension)*.</span></span>
3. <span data-ttu-id="1be40-135">在文件末尾的右 `</Project>` 标记之前，添加以下标记，以指定何时执行新的目标。</span><span class="sxs-lookup"><span data-stu-id="1be40-135">At the end of the file, before the closing `</Project>` tag, add the following markup that specifies when to execute the new target.</span></span>

    [!code-xml[Main](deploying-extra-files/samples/sample2.xml)]

    <span data-ttu-id="1be40-136">此代码会在执行将文件复制到目标文件夹的目标时执行新的 `CustomCollectFiles` 目标。</span><span class="sxs-lookup"><span data-stu-id="1be40-136">This code causes the new `CustomCollectFiles` target to be executed whenever the target that copies files to the destination folder is executed.</span></span> <span data-ttu-id="1be40-137">有一个单独的目标用于发布和部署包创建，在你决定使用部署包而不是发布来部署的情况下，新目标将注入两个目标。</span><span class="sxs-lookup"><span data-stu-id="1be40-137">There is a separate target for publish versus deployment package creation, and the new target is injected in both targets in case you decide to deploy by using a deployment package instead of publishing.</span></span>

    <span data-ttu-id="1be40-138">*.Pubxml*文件现在如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="1be40-138">The *.pubxml* file now looks like the following example:</span></span>

    [!code-xml[Main](deploying-extra-files/samples/sample3.xml?highlight=53-71)]
4. <span data-ttu-id="1be40-139">保存并关闭 *.pubxml*文件。</span><span class="sxs-lookup"><span data-stu-id="1be40-139">Save and close the *Staging.pubxml* file.</span></span>

## <a name="publish-to-staging"></a><span data-ttu-id="1be40-140">发布到过渡</span><span class="sxs-lookup"><span data-stu-id="1be40-140">Publish to staging</span></span>

<span data-ttu-id="1be40-141">使用一键式发布或命令行，使用临时配置文件发布应用程序。</span><span class="sxs-lookup"><span data-stu-id="1be40-141">Using one-click publish or the command line, publish the application by using the Staging profile.</span></span>

<span data-ttu-id="1be40-142">如果使用一键式发布，则可以在**预览**窗口中验证是否将复制*机器人。*</span><span class="sxs-lookup"><span data-stu-id="1be40-142">If you use one-click publish, you can verify in the **Preview** window that *robots.txt* will be copied.</span></span> <span data-ttu-id="1be40-143">否则，请使用 FTP 工具来验证*机器人 .txt*文件是否在部署后位于该网站的根文件夹中。</span><span class="sxs-lookup"><span data-stu-id="1be40-143">Otherwise, use your FTP tool to verify that the *robots.txt* file is in the root folder of the web site after deployment.</span></span>

## <a name="summary"></a><span data-ttu-id="1be40-144">总结</span><span class="sxs-lookup"><span data-stu-id="1be40-144">Summary</span></span>

<span data-ttu-id="1be40-145">这将完成这一系列教程，介绍如何将 ASP.NET web 应用程序部署到第三方托管提供程序。</span><span class="sxs-lookup"><span data-stu-id="1be40-145">This completes this series of tutorials on deploying an ASP.NET web application to a third-party hosting provider.</span></span> <span data-ttu-id="1be40-146">有关这些教程中所涉及的任何主题的详细信息，请参阅[ASP.NET 部署内容映射](https://go.microsoft.com/fwlink/p/?LinkId=282413)。</span><span class="sxs-lookup"><span data-stu-id="1be40-146">For more information about any of the topics covered in these tutorials, see the [ASP.NET Deployment Content Map](https://go.microsoft.com/fwlink/p/?LinkId=282413).</span></span>

## <a name="more-information"></a><span data-ttu-id="1be40-147">更多信息</span><span class="sxs-lookup"><span data-stu-id="1be40-147">More information</span></span>

<span data-ttu-id="1be40-148">如果你知道如何使用 MSBuild 文件，则可以通过在 *.pubxml*文件中（对于特定于配置文件的任务）或项目*wpp*文件（适用于适用于所有配置文件的任务）编写代码来自动执行许多其他部署任务。</span><span class="sxs-lookup"><span data-stu-id="1be40-148">If you know how to work with MSBuild files, you can automate many other deployment tasks by writing code in *.pubxml* files (for profile-specific tasks) or the project *.wpp.targets* file (for tasks that apply to all profiles).</span></span> <span data-ttu-id="1be40-149">有关 *.pubxml*和 .pubxml 文件的详细*信息，请*参阅[如何：在发布配置文件中编辑部署设置（.）文件和 Visual Studio Web 项目中的文件](https://msdn.microsoft.com/library/ff398069)。</span><span class="sxs-lookup"><span data-stu-id="1be40-149">For more information about *.pubxml* and *.wpp.targets* files, see [How to: Edit Deployment Settings in Publish Profile (.pubxml) Files and the .wpp.targets File in Visual Studio Web Projects](https://msdn.microsoft.com/library/ff398069).</span></span> <span data-ttu-id="1be40-150">有关 MSBuild 代码的基本介绍，请参阅企业部署系列中的**项目文件解析** [：了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)。</span><span class="sxs-lookup"><span data-stu-id="1be40-150">For a basic introduction to MSBuild code, see **The Anatomy of a Project File** in [Enterprise Deployment Series: Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md).</span></span> <span data-ttu-id="1be40-151">若要了解如何使用 MSBuild 文件来为自己的方案执行任务，请参阅此书籍：在[Microsoft 生成引擎：使用 MSBuild 和 Team Foundation build](http://msbuildbook.com) By Sayed Ibraham Hashimi 和 William Bartholomew。</span><span class="sxs-lookup"><span data-stu-id="1be40-151">To learn how to work with MSBuild files to perform tasks for your own scenarios, see this book: [Inside the Microsoft Build Engine: Using MSBuild and Team Foundation Build](http://msbuildbook.com) by Sayed Ibraham Hashimi and William Bartholomew.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="1be40-152">致谢</span><span class="sxs-lookup"><span data-stu-id="1be40-152">Acknowledgements</span></span>

<span data-ttu-id="1be40-153">我想感谢以下人员对本系列教程的内容进行了重大贡献：</span><span class="sxs-lookup"><span data-stu-id="1be40-153">I would like to thank the following people who made significant contributions to the content of this tutorial series:</span></span>

- [<span data-ttu-id="1be40-154">Alberto Poblacion，MVP &amp; MCT，西班牙</span><span class="sxs-lookup"><span data-stu-id="1be40-154">Alberto Poblacion, MVP &amp; MCT, Spain</span></span>](https://mvp.microsoft.com/mvp/Alberto%20Poblacion%20Bolano-36772)
- <span data-ttu-id="1be40-155">Jarod Ferguson，数据平台开发 MVP，美国</span><span class="sxs-lookup"><span data-stu-id="1be40-155">Jarod Ferguson, Data Platform Development MVP, United States</span></span>
- <span data-ttu-id="1be40-156">恶劣 Mittal，Microsoft</span><span class="sxs-lookup"><span data-stu-id="1be40-156">Harsh Mittal, Microsoft</span></span>
- <span data-ttu-id="1be40-157">[吴建 Galloway](https://weblogs.asp.net/jgalloway) （twitter： [@jongalloway](http://twitter.com/jongalloway)）</span><span class="sxs-lookup"><span data-stu-id="1be40-157">[Jon Galloway](https://weblogs.asp.net/jgalloway) (twitter: [@jongalloway](http://twitter.com/jongalloway))</span></span>
- [<span data-ttu-id="1be40-158">Kristina Olson，Microsoft</span><span class="sxs-lookup"><span data-stu-id="1be40-158">Kristina Olson, Microsoft</span></span>](https://blogs.iis.net/krolson/default.aspx)
- [<span data-ttu-id="1be40-159">Mike Pope，Microsoft</span><span class="sxs-lookup"><span data-stu-id="1be40-159">Mike Pope, Microsoft</span></span>](http://www.mikepope.com/blog/DisplayBlog.aspx)
- <span data-ttu-id="1be40-160">Mohit Srivastava，Microsoft</span><span class="sxs-lookup"><span data-stu-id="1be40-160">Mohit Srivastava, Microsoft</span></span>
- [<span data-ttu-id="1be40-161">Raffaele Rialdi，意大利</span><span class="sxs-lookup"><span data-stu-id="1be40-161">Raffaele Rialdi, Italy</span></span>](http://www.iamraf.net/)
- [<span data-ttu-id="1be40-162">Microsoft Rick Anderson</span><span class="sxs-lookup"><span data-stu-id="1be40-162">Rick Anderson, Microsoft</span></span>](https://blogs.msdn.com/b/rickandy/)
- <span data-ttu-id="1be40-163">[Sayed Hashimi，Microsoft](http://sedodream.com/default.aspx)（twitter： [@sayedihashimi](http://twitter.com/sayedihashimi)）</span><span class="sxs-lookup"><span data-stu-id="1be40-163">[Sayed Hashimi, Microsoft](http://sedodream.com/default.aspx)(twitter: [@sayedihashimi](http://twitter.com/sayedihashimi))</span></span>
- <span data-ttu-id="1be40-164">[Scott Hanselman](http://www.hanselman.com/blog/) （twitter： [@shanselman](http://twitter.com/shanselman)）</span><span class="sxs-lookup"><span data-stu-id="1be40-164">[Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [@shanselman](http://twitter.com/shanselman))</span></span>
- <span data-ttu-id="1be40-165">[Scott Hunter，Microsoft](https://blogs.msdn.com/b/scothu/) （twitter： [@coolcsh](http://twitter.com/coolcsh)）</span><span class="sxs-lookup"><span data-stu-id="1be40-165">[Scott Hunter, Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [@coolcsh](http://twitter.com/coolcsh))</span></span>
- [<span data-ttu-id="1be40-166">Srđan Božović，塞尔维亚</span><span class="sxs-lookup"><span data-stu-id="1be40-166">Srđan Božović, Serbia</span></span>](http://msforge.net/blogs/zmajcek/)
- <span data-ttu-id="1be40-167">[Vishal Joshi，Microsoft](http://vishaljoshi.blogspot.com/) （twitter： [@vishalrjoshi](http://twitter.com/vishalrjoshi)）</span><span class="sxs-lookup"><span data-stu-id="1be40-167">[Vishal Joshi, Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [@vishalrjoshi](http://twitter.com/vishalrjoshi))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1be40-168">[上一页](command-line-deployment.md)
> [下一页](troubleshooting.md)</span><span class="sxs-lookup"><span data-stu-id="1be40-168">[Previous](command-line-deployment.md)
[Next](troubleshooting.md)</span></span>
