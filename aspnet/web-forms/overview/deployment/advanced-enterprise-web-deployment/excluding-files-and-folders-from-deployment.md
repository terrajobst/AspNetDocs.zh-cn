---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/excluding-files-and-folders-from-deployment
title: 从部署中排除文件和文件夹 |Microsoft Docs
author: jrjlee
description: 本主题介绍在生成和打包 web 应用程序项目时，如何从 web 部署包中排除文件和文件夹。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: f4cc2d40-6a78-429b-b06f-07d000d4caad
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/excluding-files-and-folders-from-deployment
msc.type: authoredcontent
ms.openlocfilehash: a262ce43d7199fb1015d54d0b7c213857c360946
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78438416"
---
# <a name="excluding-files-and-folders-from-deployment"></a><span data-ttu-id="dff3e-103">从部署中排除文件和文件夹</span><span class="sxs-lookup"><span data-stu-id="dff3e-103">Excluding Files and Folders from Deployment</span></span>

<span data-ttu-id="dff3e-104">作者： [Jason](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="dff3e-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="dff3e-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="dff3e-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="dff3e-106">本主题介绍在生成和打包 web 应用程序项目时，如何从 web 部署包中排除文件和文件夹。</span><span class="sxs-lookup"><span data-stu-id="dff3e-106">This topic describes how you can exclude files and folders from a web deployment package when you build and package a web application project.</span></span>

<span data-ttu-id="dff3e-107">本主题介绍一系列教程的一部分，这些教程基于名为 Fabrikam，Inc. 的虚构公司的企业部署要求。本教程系列使用一个示例解决方案&#x2014;，该解决方案使用[联系人管理器解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示具有真实复杂性级别的 web 应用程序，包括 ASP.NET MVC 3 应用程序、Windows Communication Foundation （WCF）服务和数据库项目。</span><span class="sxs-lookup"><span data-stu-id="dff3e-107">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="dff3e-108">这些教程核心的部署方法基于[理解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)中所述的拆分项目文件方法，其中，生成过程由两个项目文件&#x2014;控制，其中一个包含适用于每个目标环境的生成说明，另一个包含特定于环境的生成和部署设置。</span><span class="sxs-lookup"><span data-stu-id="dff3e-108">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="dff3e-109">在生成时，特定于环境的项目文件将合并到环境无关的项目文件中，以形成一组完整的生成说明。</span><span class="sxs-lookup"><span data-stu-id="dff3e-109">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="overview"></a><span data-ttu-id="dff3e-110">概述</span><span class="sxs-lookup"><span data-stu-id="dff3e-110">Overview</span></span>

<span data-ttu-id="dff3e-111">当您在 Visual Studio 2010 中生成 web 应用程序项目时，Web 发布管道（WPP）允许您通过将已编译的 web 应用程序打包到可部署的 web 包中来扩展此生成过程。</span><span class="sxs-lookup"><span data-stu-id="dff3e-111">When you build a web application project in Visual Studio 2010, the Web Publishing Pipeline (WPP) lets you extend this build process by packaging your compiled web application into a deployable web package.</span></span> <span data-ttu-id="dff3e-112">然后，可以使用 Internet Information Services （IIS） Web 部署工具（Web 部署）将此 web 包部署到远程 IIS web 服务器，或通过 IIS 管理器手动导入 web 包。</span><span class="sxs-lookup"><span data-stu-id="dff3e-112">You can then use the Internet Information Services (IIS) Web Deployment Tool (Web Deploy) to deploy this web package to a remote IIS web server, or import the web package manually through IIS Manager.</span></span> <span data-ttu-id="dff3e-113">此打包过程在[生成和打包 Web 应用程序项目](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)中进行了介绍。</span><span class="sxs-lookup"><span data-stu-id="dff3e-113">This packaging process is explained in [Building and Packaging Web Application Projects](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md).</span></span>

<span data-ttu-id="dff3e-114">那么，如何控制 web 包中包含的内容呢？</span><span class="sxs-lookup"><span data-stu-id="dff3e-114">So how do you control what gets included in your web package?</span></span> <span data-ttu-id="dff3e-115">Visual Studio 中的项目设置，通过基础项目文件，为很多方案提供足够的控制权。</span><span class="sxs-lookup"><span data-stu-id="dff3e-115">The project settings in Visual Studio, through the underlying project file, provide sufficient control for a lot of scenarios.</span></span> <span data-ttu-id="dff3e-116">但是，在某些情况下，可能需要将 web 包的内容定制为特定的目标环境。</span><span class="sxs-lookup"><span data-stu-id="dff3e-116">However, in some cases you may want to tailor the contents of your web package to specific destination environments.</span></span> <span data-ttu-id="dff3e-117">例如，你可能想要在将应用程序部署到测试环境时包括日志文件的文件夹，但在将应用程序部署到过渡环境或生产环境时排除文件夹。</span><span class="sxs-lookup"><span data-stu-id="dff3e-117">For example, you might want to include a folder for log files when you deploy your application to a test environment but exclude the folder when you deploy the application to a staging or production environment.</span></span> <span data-ttu-id="dff3e-118">本主题将演示如何执行此操作。</span><span class="sxs-lookup"><span data-stu-id="dff3e-118">This topic will show you how to do this.</span></span>

## <a name="what-gets-included-by-default"></a><span data-ttu-id="dff3e-119">默认情况下包含哪些内容？</span><span class="sxs-lookup"><span data-stu-id="dff3e-119">What Gets Included by Default?</span></span>

<span data-ttu-id="dff3e-120">当你在 Visual Studio 中配置你的 web 应用程序项目属性时，"**包/发布**" 网页上的 "**要部署的项目**" 列表使你可以指定要包括在 web 部署包中的内容。</span><span class="sxs-lookup"><span data-stu-id="dff3e-120">When you configure your web application project properties in Visual Studio, the **Items to deploy** list on the **Package/Publish Web** page lets you specify what you want to include in your web deployment package.</span></span> <span data-ttu-id="dff3e-121">默认情况下，此设置为**仅限运行此应用程序所需的文件**。</span><span class="sxs-lookup"><span data-stu-id="dff3e-121">By default, this is set to **Only files needed to run this application**.</span></span>

![](excluding-files-and-folders-from-deployment/_static/image1.png)

<span data-ttu-id="dff3e-122">如果仅选择**运行此应用程序所需的文件**，WPP 将尝试确定哪些文件应添加到 web 包中。</span><span class="sxs-lookup"><span data-stu-id="dff3e-122">When you choose **Only files needed to run this application**, the WPP will try to determine which files should be added to the web package.</span></span> <span data-ttu-id="dff3e-123">这包括：</span><span class="sxs-lookup"><span data-stu-id="dff3e-123">This includes:</span></span>

- <span data-ttu-id="dff3e-124">项目的所有生成输出。</span><span class="sxs-lookup"><span data-stu-id="dff3e-124">All the build outputs for the project.</span></span>
- <span data-ttu-id="dff3e-125">任何标记有**Content**的生成操作的文件。</span><span class="sxs-lookup"><span data-stu-id="dff3e-125">Any files marked with a build action of **Content**.</span></span>

> [!NOTE]
> <span data-ttu-id="dff3e-126">确定要包含的文件的逻辑包含在此文件中：</span><span class="sxs-lookup"><span data-stu-id="dff3e-126">The logic that determines which files to include is contained in this file:</span></span>   
> <span data-ttu-id="dff3e-127">*%PROGRAMFILES%\MSBuild\Microsoft\VisualStudio\v10.0\Web\ （OnlyFilesToRunTheApp）*</span><span class="sxs-lookup"><span data-stu-id="dff3e-127">*%PROGRAMFILES%\MSBuild\Microsoft\VisualStudio\v10.0\Web\ Microsoft.Web.Publishing.OnlyFilesToRunTheApp.targets*</span></span>

## <a name="excluding-specific-files-and-folders"></a><span data-ttu-id="dff3e-128">排除特定的文件和文件夹</span><span class="sxs-lookup"><span data-stu-id="dff3e-128">Excluding Specific Files and Folders</span></span>

<span data-ttu-id="dff3e-129">在某些情况下，您需要更精细地控制部署哪些文件和文件夹。</span><span class="sxs-lookup"><span data-stu-id="dff3e-129">In some cases, you'll want more fine-grained control over which files and folders are deployed.</span></span> <span data-ttu-id="dff3e-130">如果您知道您要提前排除哪些文件，并且排除适用于所有目标环境，则您可以简单地将每个文件的**生成操作**设置为 "**无**"。</span><span class="sxs-lookup"><span data-stu-id="dff3e-130">If you know which files you want to exclude ahead of time, and the exclusion applies to all destination environments, you can simply set the **Build Action** of each file to **None**.</span></span>

<span data-ttu-id="dff3e-131">**从部署中排除特定文件**</span><span class="sxs-lookup"><span data-stu-id="dff3e-131">**To exclude specific files from deployment**</span></span>

1. <span data-ttu-id="dff3e-132">在 "**解决方案资源管理器**" 窗口中，右键单击该文件，然后单击 "**属性**"。</span><span class="sxs-lookup"><span data-stu-id="dff3e-132">In the **Solution Explorer** window, right-click the file, and then click **Properties**.</span></span>
2. <span data-ttu-id="dff3e-133">在 "**属性**" 窗口的 "**生成操作**" 行中，选择 "**无**"。</span><span class="sxs-lookup"><span data-stu-id="dff3e-133">In the **Properties** window, in the **Build Action** row, select **None**.</span></span>

<span data-ttu-id="dff3e-134">但是，这种方法并不是很方便。</span><span class="sxs-lookup"><span data-stu-id="dff3e-134">However, this approach is not always convenient.</span></span> <span data-ttu-id="dff3e-135">例如，你可能想要根据目标环境以及从 Visual Studio 外部包含哪些文件和文件夹。</span><span class="sxs-lookup"><span data-stu-id="dff3e-135">For example, you may want to vary which files and folders are included according to your destination environment, and from outside Visual Studio.</span></span> <span data-ttu-id="dff3e-136">例如，在 "联系人管理器" 示例解决方案中，查看 ContactManager 项目的内容：</span><span class="sxs-lookup"><span data-stu-id="dff3e-136">For example, in the Contact Manager sample solution, take a look at the contents of the ContactManager.Mvc project:</span></span>

![](excluding-files-and-folders-from-deployment/_static/image2.png)

- <span data-ttu-id="dff3e-137">内部文件夹包含一些 SQL 脚本，开发人员可以使用这些脚本来创建、删除和填充用于开发的本地数据库。</span><span class="sxs-lookup"><span data-stu-id="dff3e-137">The Internal folder contains some SQL scripts that the developer uses to create, drop, and populate local databases for development purposes.</span></span> <span data-ttu-id="dff3e-138">应将此文件夹中的任何内容部署到过渡环境或生产环境中。</span><span class="sxs-lookup"><span data-stu-id="dff3e-138">Nothing in this folder should be deployed to a staging or production environment.</span></span>
- <span data-ttu-id="dff3e-139">Scripts 文件夹包含多个 JavaScript 文件。</span><span class="sxs-lookup"><span data-stu-id="dff3e-139">The Scripts folder contains several JavaScript files.</span></span> <span data-ttu-id="dff3e-140">其中的许多文件纯粹是为了支持调试或在 Visual Studio 中提供 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="dff3e-140">A lot of these files are included purely to support debugging or provide IntelliSense in Visual Studio.</span></span> <span data-ttu-id="dff3e-141">其中一些文件不应部署到过渡环境或生产环境中。</span><span class="sxs-lookup"><span data-stu-id="dff3e-141">Some of these files should not be deployed to staging or production environments.</span></span> <span data-ttu-id="dff3e-142">但是，你可能希望将它们部署到开发人员测试环境中，以便于进行故障排除。</span><span class="sxs-lookup"><span data-stu-id="dff3e-142">However, you may want to deploy them to a developer test environment to facilitate troubleshooting.</span></span>

<span data-ttu-id="dff3e-143">虽然您可以操作项目文件以排除特定文件和文件夹，但有一种更简单的方法。</span><span class="sxs-lookup"><span data-stu-id="dff3e-143">Although you could manipulate your project files to exclude specific files and folders, there is an easier way.</span></span> <span data-ttu-id="dff3e-144">WPP 包含一种机制，可通过生成名为**ExcludeFromPackageFolders**和**ExcludeFromPackageFiles**的项列表来排除文件和文件夹。</span><span class="sxs-lookup"><span data-stu-id="dff3e-144">The WPP includes a mechanism to exclude files and folders by building item lists named **ExcludeFromPackageFolders** and **ExcludeFromPackageFiles**.</span></span> <span data-ttu-id="dff3e-145">您可以通过将您自己的项添加到这些列表来扩展此机制。</span><span class="sxs-lookup"><span data-stu-id="dff3e-145">You can extend this mechanism by adding your own items to these lists.</span></span> <span data-ttu-id="dff3e-146">要执行此操作，需要完成以下高级步骤：</span><span class="sxs-lookup"><span data-stu-id="dff3e-146">To do this, you need to complete these high-level steps:</span></span>

1. <span data-ttu-id="dff3e-147">在与项目文件相同的文件夹中创建一个名为 *[项目名称]* 的自定义项目文件。</span><span class="sxs-lookup"><span data-stu-id="dff3e-147">Create a custom project file named *[project name].wpp.targets* in the same folder as your project file.</span></span>

    > [!NOTE]
    > <span data-ttu-id="dff3e-148">.Csproj&#x2014;文件需要与你的 web 应用程序*项目文件*&#x2014;位于同一文件夹中，例如， *ContactManager*，而不是与你用来控制生成和部署过程的任何自定义项目文件位于同一文件夹中。</span><span class="sxs-lookup"><span data-stu-id="dff3e-148">The *.wpp.targets* file needs to go in the same folder as your web application project file&#x2014;for example, *ContactManager.Mvc.csproj*&#x2014;rather than in the same folder as any custom project files you use to control the build and deployment process.</span></span>
2. <span data-ttu-id="dff3e-149">在 *. .targets*文件中，添加一个**ItemGroup**元素。</span><span class="sxs-lookup"><span data-stu-id="dff3e-149">In the *.wpp.targets* file, add an **ItemGroup** element.</span></span>
3. <span data-ttu-id="dff3e-150">在**ItemGroup**元素中，添加**ExcludeFromPackageFolders**和**ExcludeFromPackageFiles**项，以根据需要排除特定的文件和文件夹。</span><span class="sxs-lookup"><span data-stu-id="dff3e-150">In the **ItemGroup** element, add **ExcludeFromPackageFolders** and **ExcludeFromPackageFiles** items to exclude specific files and folders as required.</span></span>

<span data-ttu-id="dff3e-151">*这是此文件的*基本结构：</span><span class="sxs-lookup"><span data-stu-id="dff3e-151">This is the basic structure of this *.wpp.targets* file:</span></span>

[!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample1.xml)]

<span data-ttu-id="dff3e-152">请注意，每个项都包含名为**FromTarget**的项元数据元素。</span><span class="sxs-lookup"><span data-stu-id="dff3e-152">Note that each item includes an item metadata element named **FromTarget**.</span></span> <span data-ttu-id="dff3e-153">这是一个可选值，不会影响生成过程;它仅用于指示当有人查看生成日志时省略特定文件或文件夹的原因。</span><span class="sxs-lookup"><span data-stu-id="dff3e-153">This is an optional value that doesn't affect the build process; it simply serves to indicate why particular files or folders were omitted if someone reviews the build logs.</span></span>

## <a name="excluding-files-and-folders-from-a-web-package"></a><span data-ttu-id="dff3e-154">从 Web 包中排除文件和文件夹</span><span class="sxs-lookup"><span data-stu-id="dff3e-154">Excluding Files and Folders from a Web Package</span></span>

<span data-ttu-id="dff3e-155">下一过程演示了如何在生成项目时，将*wpp*文件添加到 web 应用程序项目，以及如何使用该文件从 web 包中排除特定的文件和文件夹。</span><span class="sxs-lookup"><span data-stu-id="dff3e-155">The next procedure shows you how to add a *.wpp.targets* file to a web application project and how to use the file to exclude specific files and folders from the web package when you build your project.</span></span>

<span data-ttu-id="dff3e-156">**从 web 部署包中排除文件和文件夹**</span><span class="sxs-lookup"><span data-stu-id="dff3e-156">**To exclude files and folders from a web deployment package**</span></span>

1. <span data-ttu-id="dff3e-157">在 Visual Studio 2010 中打开解决方案。</span><span class="sxs-lookup"><span data-stu-id="dff3e-157">Open your solution in Visual Studio 2010.</span></span>
2. <span data-ttu-id="dff3e-158">在 "**解决方案资源管理器**" 窗口中，右键单击 web 应用程序项目节点（例如**ContactManager**），指向 "**添加**"，然后单击 "**新建项**"。</span><span class="sxs-lookup"><span data-stu-id="dff3e-158">In the **Solution Explorer** window, right-click your web application project node (for example, **ContactManager.Mvc**), point to **Add**, and then click **New Item**.</span></span>
3. <span data-ttu-id="dff3e-159">在 "**添加新项**" 对话框中，选择 " **XML 文件**" 模板。</span><span class="sxs-lookup"><span data-stu-id="dff3e-159">In the **Add New Item** dialog box, select the **XML File** template.</span></span>
4. <span data-ttu-id="dff3e-160">在 "**名称**" 框中，键入 *[项目名称] \* *. wpp** （例如， **ContactManager**），然后单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="dff3e-160">In the **Name** box, type *[project name]\*\*\*.wpp.targets*\* (for example, **ContactManager.Mvc.wpp.targets**), and then click **Add**.</span></span>

    ![](excluding-files-and-folders-from-deployment/_static/image3.png)

    > [!NOTE]
    > <span data-ttu-id="dff3e-161">如果将新项添加到项目的根节点，则会在与项目文件相同的文件夹中创建该文件。</span><span class="sxs-lookup"><span data-stu-id="dff3e-161">If you add a new item to the root node of a project, the file is created in the same folder as the project file.</span></span> <span data-ttu-id="dff3e-162">可以通过在 Windows 资源管理器中打开该文件夹来验证这一点。</span><span class="sxs-lookup"><span data-stu-id="dff3e-162">You can verify this by opening the folder in Windows Explorer.</span></span>
5. <span data-ttu-id="dff3e-163">在文件中，添加**项目**元素和**ItemGroup**元素：</span><span class="sxs-lookup"><span data-stu-id="dff3e-163">In the file, add a **Project** element and an **ItemGroup** element:</span></span>

    [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample2.xml)]
6. <span data-ttu-id="dff3e-164">如果要从 web 包中排除文件夹，请将**ExcludeFromPackageFolders**元素添加到**ItemGroup**元素：</span><span class="sxs-lookup"><span data-stu-id="dff3e-164">If you want to exclude folders from the web package, add an **ExcludeFromPackageFolders** element to the **ItemGroup** element:</span></span>

   1. <span data-ttu-id="dff3e-165">在**Include**特性中，提供要排除的文件夹的分号分隔列表。</span><span class="sxs-lookup"><span data-stu-id="dff3e-165">In the **Include** attribute, provide a semicolon-separated list of the folders you want to exclude.</span></span>
   2. <span data-ttu-id="dff3e-166">在**FromTarget** metadata 元素中，提供一个有意义的值，用于指示排除文件夹的原因，例如， *.targets*文件的名称。</span><span class="sxs-lookup"><span data-stu-id="dff3e-166">In the **FromTarget** metadata element, provide a meaningful value to indicate why the folders are being excluded, like the name of the *.wpp.targets* file.</span></span>

      [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample3.xml)]
7. <span data-ttu-id="dff3e-167">如果要从 web 包中排除文件，请将**ExcludeFromPackageFiles**元素添加到**ItemGroup**元素：</span><span class="sxs-lookup"><span data-stu-id="dff3e-167">If you want to exclude files from the web package, add an **ExcludeFromPackageFiles** element to the **ItemGroup** element:</span></span>

   1. <span data-ttu-id="dff3e-168">在**Include**特性中，提供要排除的文件的列表（以分号分隔）。</span><span class="sxs-lookup"><span data-stu-id="dff3e-168">In the **Include** attribute, provide a semicolon-separated list of the files you want to exclude.</span></span>
   2. <span data-ttu-id="dff3e-169">在**FromTarget** metadata 元素中，提供一个有意义的值，用于指示排除文件的原因，例如， *.targets*文件的名称。</span><span class="sxs-lookup"><span data-stu-id="dff3e-169">In the **FromTarget** metadata element, provide a meaningful value to indicate why the files are being excluded, like the name of the *.wpp.targets* file.</span></span>

      [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample4.xml)]
8. <span data-ttu-id="dff3e-170">*[项目名称] wpp*文件现在应如下所示：</span><span class="sxs-lookup"><span data-stu-id="dff3e-170">The *[project name].wpp.targets* file should now resemble this:</span></span>

    [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample5.xml)]
9. <span data-ttu-id="dff3e-171">保存并关闭 *[项目名称] .targets*文件。</span><span class="sxs-lookup"><span data-stu-id="dff3e-171">Save and close the *[project name].wpp.targets* file.</span></span>

<span data-ttu-id="dff3e-172">下一次生成和打包 web 应用程序项目时，WPP 会自动检测 *.targets*文件。</span><span class="sxs-lookup"><span data-stu-id="dff3e-172">The next time you build and package your web application project, the WPP will automatically detect the *.wpp.targets* file.</span></span> <span data-ttu-id="dff3e-173">您指定的任何文件和文件夹不会包含在 web 包中。</span><span class="sxs-lookup"><span data-stu-id="dff3e-173">Any files and folders you specified will not be included in the web package.</span></span>

## <a name="conclusion"></a><span data-ttu-id="dff3e-174">结束语</span><span class="sxs-lookup"><span data-stu-id="dff3e-174">Conclusion</span></span>

<span data-ttu-id="dff3e-175">本主题介绍了如何在生成 web 包时排除特定文件和文件夹，方法是在与 web 应用程序项目文件相同的文件夹中创建一个自定义的 *.targets*文件。</span><span class="sxs-lookup"><span data-stu-id="dff3e-175">This topic described how to exclude specific files and folders when you build a web package, by creating a custom *.wpp.targets* file in the same folder as your web application project file.</span></span>

## <a name="further-reading"></a><span data-ttu-id="dff3e-176">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="dff3e-176">Further Reading</span></span>

<span data-ttu-id="dff3e-177">有关使用自定义 Microsoft 生成引擎（MSBuild）项目文件来控制部署过程的详细信息，请参阅[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)和[了解生成过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)。</span><span class="sxs-lookup"><span data-stu-id="dff3e-177">For more information on using custom Microsoft Build Engine (MSBuild) project files to control the deployment process, see [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md) and [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span> <span data-ttu-id="dff3e-178">有关打包和部署过程的详细信息，请参阅[生成和打包 Web 应用程序项目](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)、[配置 web 包部署的参数](../web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment.md)和[部署 web 包](../web-deployment-in-the-enterprise/deploying-web-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="dff3e-178">For more information on the packaging and deployment process, see [Building and Packaging Web Application Projects](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md), [Configuring Parameters for Web Package Deployment](../web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment.md), and [Deploying Web Packages](../web-deployment-in-the-enterprise/deploying-web-packages.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="dff3e-179">[上一页](deploying-membership-databases-to-enterprise-environments.md)
> [下一页](taking-web-applications-offline-with-web-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="dff3e-179">[Previous](deploying-membership-databases-to-enterprise-environments.md)
[Next](taking-web-applications-offline-with-web-deploy.md)</span></span>
