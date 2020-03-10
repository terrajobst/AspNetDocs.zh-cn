---
uid: web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment
title: 使用 Visual Studio 的 ASP.NET Web 部署：命令行部署 |Microsoft Docs
author: tdykstra
description: 本系列教程介绍了如何通过来将 ASP.NET web 应用程序部署（发布）到 Azure App Service Web 应用或第三方托管提供程序。
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 82b8dea0-f062-4ee4-8784-3ffa30fbb1ca
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment
msc.type: authoredcontent
ms.openlocfilehash: 13cfe4492398b59f2c80394689cc113ccb218c60
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78512072"
---
# <a name="aspnet-web-deployment-using-visual-studio-command-line-deployment"></a><span data-ttu-id="b5944-103">使用 Visual Studio 的 ASP.NET Web 部署：命令行部署</span><span class="sxs-lookup"><span data-stu-id="b5944-103">ASP.NET Web Deployment using Visual Studio: Command Line Deployment</span></span>

<span data-ttu-id="b5944-104">作者： [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="b5944-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="b5944-105">下载初学者项目</span><span class="sxs-lookup"><span data-stu-id="b5944-105">Download Starter Project</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="b5944-106">本系列教程介绍了如何使用 Visual Studio 2012 或 Visual Studio 2010，将 ASP.NET web 应用程序部署（发布）到 Azure App Service Web 应用或第三方托管提供商。</span><span class="sxs-lookup"><span data-stu-id="b5944-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="b5944-107">有关序列的信息，请参阅本[系列中的第一个教程](introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="b5944-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="b5944-108">概述</span><span class="sxs-lookup"><span data-stu-id="b5944-108">Overview</span></span>

<span data-ttu-id="b5944-109">本教程演示如何从命令行调用 Visual Studio web 发布管道。</span><span class="sxs-lookup"><span data-stu-id="b5944-109">This tutorial shows you how to invoke the Visual Studio web publish pipeline from the command line.</span></span> <span data-ttu-id="b5944-110">这对于以下情况非常有用：您希望在 Visual Studio 中[自动执行部署过程](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md)，而不是在 Visual Studio 中手动执行此操作，通常使用[源代码版本控制系统](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md)。</span><span class="sxs-lookup"><span data-stu-id="b5944-110">This is useful for scenarios where you want to [automate the deployment process](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md) instead of doing it manually in Visual Studio, typically by using a [source code version control system](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md).</span></span>

## <a name="make-a-change-to-deploy"></a><span data-ttu-id="b5944-111">进行部署更改</span><span class="sxs-lookup"><span data-stu-id="b5944-111">Make a change to deploy</span></span>

<span data-ttu-id="b5944-112">当前 "关于" 页显示模板代码。</span><span class="sxs-lookup"><span data-stu-id="b5944-112">Currently the About page displays the template code.</span></span>

![带有模板代码的 "关于" 页](command-line-deployment/_static/image1.png)

<span data-ttu-id="b5944-114">你需要将其替换为显示学生注册摘要的代码。</span><span class="sxs-lookup"><span data-stu-id="b5944-114">You'll replace that with code that displays a summary of student enrollment.</span></span>

<span data-ttu-id="b5944-115">打开*About*页，删除 `MainContent` `Content` 元素内的所有标记，并在其位置插入以下标记：</span><span class="sxs-lookup"><span data-stu-id="b5944-115">Open the *About.aspx* page, delete all of the markup inside the `MainContent` `Content` element, and insert the following markup in its place:</span></span>

[!code-aspx[Main](command-line-deployment/samples/sample1.aspx)]

<span data-ttu-id="b5944-116">运行该项目并选择 "**关于**" 页。</span><span class="sxs-lookup"><span data-stu-id="b5944-116">Run the project and select the **About** page.</span></span>

![“关于”页面](command-line-deployment/_static/image2.png)

## <a name="deploy-to-test-by-using-the-command-line"></a><span data-ttu-id="b5944-118">使用命令行部署到测试</span><span class="sxs-lookup"><span data-stu-id="b5944-118">Deploy to Test by using the command line</span></span>

<span data-ttu-id="b5944-119">你不会部署其他数据库更改，因此请对 ContosoUniversity 数据库禁用 dbDacFx 数据库部署。</span><span class="sxs-lookup"><span data-stu-id="b5944-119">You won't be deploying another database change, so disable dbDacFx database deployment for the aspnet-ContosoUniversity database.</span></span> <span data-ttu-id="b5944-120">打开 "**发布 Web** " 向导，并在三个发布配置文件中的每一个配置文件中，清除 "**设置**" 选项卡上的 "**更新数据库**" 复选框。</span><span class="sxs-lookup"><span data-stu-id="b5944-120">Open the **Publish Web** wizard, and in each of the three publish profiles, clear the **Update Database** check box on the **Settings** tab.</span></span>

<span data-ttu-id="b5944-121">在 Windows 8 "开始" 页中，搜索**VS2012 的开发人员命令提示**。</span><span class="sxs-lookup"><span data-stu-id="b5944-121">In the Windows 8 Start page, search for **Developer Command Prompt for VS2012**.</span></span>

<span data-ttu-id="b5944-122">右键单击**VS2012 开发人员命令提示的**图标，然后单击 "以**管理员身份运行**"。</span><span class="sxs-lookup"><span data-stu-id="b5944-122">Right-click the icon for **Developer Command Prompt for VS2012** and click **Run as administrator**.</span></span>

<span data-ttu-id="b5944-123">在命令提示符下输入以下命令，将解决方案文件的路径替换为解决方案文件的路径：</span><span class="sxs-lookup"><span data-stu-id="b5944-123">Enter the following command at the command prompt, replacing the path to the solution file with the path to your solution file:</span></span>

[!code-console[Main](command-line-deployment/samples/sample2.cmd)]

<span data-ttu-id="b5944-124">MSBuild 生成解决方案并将其部署到测试环境。</span><span class="sxs-lookup"><span data-stu-id="b5944-124">MSBuild builds the solution and deploys it to the test environment.</span></span>

![命令行输出](command-line-deployment/_static/image3.png)

<span data-ttu-id="b5944-126">打开浏览器并中转到 `http://localhost/ContosoUniversity`，然后单击 "**关于**" 页以验证部署是否成功。</span><span class="sxs-lookup"><span data-stu-id="b5944-126">Open a browser and go to `http://localhost/ContosoUniversity`, then click the **About** page to verify that the deployment was successful.</span></span>

<span data-ttu-id="b5944-127">如果尚未创建任何学生进行测试，你会在 "**学生正文统计信息**" 标题下看到一个空页面。</span><span class="sxs-lookup"><span data-stu-id="b5944-127">If you haven't created any students in test, you'll see an empty page under the **Student Body Statistics** heading.</span></span> <span data-ttu-id="b5944-128">请访问 "**学生**" 页，单击 "**添加学生**" 并添加一些学生，然后返回到 "**关于**" 页查看学生统计信息。</span><span class="sxs-lookup"><span data-stu-id="b5944-128">Go to the **Students** page, click **Add Student**, and add some students, and then return to the **About** page to see student statistics.</span></span>

![测试环境中的 "关于" 页](command-line-deployment/_static/image4.png)

## <a name="key-command-line-options"></a><span data-ttu-id="b5944-130">密钥命令行选项</span><span class="sxs-lookup"><span data-stu-id="b5944-130">Key command line options</span></span>

<span data-ttu-id="b5944-131">你输入的命令将解决方案文件路径和两个属性传递到 MSBuild：</span><span class="sxs-lookup"><span data-stu-id="b5944-131">The command that you entered passed the solution file path and two properties to MSBuild:</span></span>

[!code-console[Main](command-line-deployment/samples/sample3.cmd)]

### <a name="deploying-the-solution-versus-deploying-individual-projects"></a><span data-ttu-id="b5944-132">部署解决方案与部署单个项目</span><span class="sxs-lookup"><span data-stu-id="b5944-132">Deploying the solution versus deploying individual projects</span></span>

<span data-ttu-id="b5944-133">指定解决方案文件将导致生成解决方案中的所有项目。</span><span class="sxs-lookup"><span data-stu-id="b5944-133">Specifying the solution file causes all projects in the solution to be built.</span></span> <span data-ttu-id="b5944-134">如果解决方案中有多个 web 项目，则以下 MSBuild 行为适用：</span><span class="sxs-lookup"><span data-stu-id="b5944-134">If you have multiple web projects in the solution, the following MSBuild behavior applies:</span></span>

- <span data-ttu-id="b5944-135">在命令行上指定的属性将传递给每个项目。</span><span class="sxs-lookup"><span data-stu-id="b5944-135">The properties that you specify on the command line are passed to every project.</span></span> <span data-ttu-id="b5944-136">因此，每个 web 项目都必须具有您指定的名称的发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="b5944-136">Therefore, each web project must have a publish profile with the name that you specify.</span></span> <span data-ttu-id="b5944-137">如果指定 `/p:PublishProfile=Test`，则每个 web 项目必须具有名为*Test*的发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="b5944-137">If you specify `/p:PublishProfile=Test`, each web project must have a publish profile named *Test*.</span></span>
- <span data-ttu-id="b5944-138">如果一个项目甚至没有生成，你可能会成功发布一个项目。</span><span class="sxs-lookup"><span data-stu-id="b5944-138">You might successfully publish one project when another one doesn't even build.</span></span> <span data-ttu-id="b5944-139">有关详细信息，请参阅 stackoverflow 线程[MSBuild with 两个包失败](http://stackoverflow.com/questions/14226451/msbuild-fails-with-two-packages)。</span><span class="sxs-lookup"><span data-stu-id="b5944-139">For more information, see the stackoverflow thread [MSBuild fails with two packages](http://stackoverflow.com/questions/14226451/msbuild-fails-with-two-packages).</span></span>

<span data-ttu-id="b5944-140">如果指定单个项目而不是解决方案，则必须添加一个指定 Visual Studio 版本的参数。</span><span class="sxs-lookup"><span data-stu-id="b5944-140">If you specify an individual project instead of a solution, you have to add a parameter that specifies the Visual Studio version.</span></span> <span data-ttu-id="b5944-141">如果使用的是 Visual Studio 2012，命令行将类似于以下示例：</span><span class="sxs-lookup"><span data-stu-id="b5944-141">If you are using Visual Studio 2012 the command line would be similar to the following example:</span></span>

[!code-console[Main](command-line-deployment/samples/sample4.cmd?highlight=1)]

<span data-ttu-id="b5944-142">Visual Studio 2010 的版本号为10.0。</span><span class="sxs-lookup"><span data-stu-id="b5944-142">The version number for Visual Studio 2010 is 10.0.</span></span> <span data-ttu-id="b5944-143">有关详细信息，请参阅[Visual Studio 项目兼容性和](http://sedodream.com/2012/08/19/VisualStudioProjectCompatabilityAndVisualStudioVersion.aspx)Sayed Hashimi 的博客上的 VisualStudioVersion。</span><span class="sxs-lookup"><span data-stu-id="b5944-143">For more information, see [Visual Studio project compatibility and VisualStudioVersion](http://sedodream.com/2012/08/19/VisualStudioProjectCompatabilityAndVisualStudioVersion.aspx) on Sayed Hashimi's blog.</span></span>

### <a name="specifying-the-publish-profile"></a><span data-ttu-id="b5944-144">指定发布配置文件</span><span class="sxs-lookup"><span data-stu-id="b5944-144">Specifying the publish profile</span></span>

<span data-ttu-id="b5944-145">可以按名称或 *.pubxml*文件的完整路径指定发布配置文件，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="b5944-145">You can specify the publish profile by name or by the full path to the *.pubxml* file, as shown in the following example:</span></span>

[!code-console[Main](command-line-deployment/samples/sample5.cmd?highlight=1)]

### <a name="web-publish-methods-supported-for-command-line-publishing"></a><span data-ttu-id="b5944-146">支持命令行发布的 Web 发布方法</span><span class="sxs-lookup"><span data-stu-id="b5944-146">Web publish methods supported for command-line publishing</span></span>

<span data-ttu-id="b5944-147">对于命令行发布，支持三种发布方法：</span><span class="sxs-lookup"><span data-stu-id="b5944-147">Three publish methods are supported for command line publishing:</span></span>

- <span data-ttu-id="b5944-148">`MSDeploy`-使用 Web 部署发布。</span><span class="sxs-lookup"><span data-stu-id="b5944-148">`MSDeploy` - Publish by using Web Deploy.</span></span>
- <span data-ttu-id="b5944-149">`Package`-通过创建 Web 部署包进行发布。</span><span class="sxs-lookup"><span data-stu-id="b5944-149">`Package` - Publish by creating a Web Deploy Package.</span></span> <span data-ttu-id="b5944-150">必须从创建包的 MSBuild 命令单独安装包。</span><span class="sxs-lookup"><span data-stu-id="b5944-150">You have to install the package separately from the MSBuild command that creates it.</span></span>
- <span data-ttu-id="b5944-151">`FileSystem`-通过将文件复制到指定的文件夹来发布。</span><span class="sxs-lookup"><span data-stu-id="b5944-151">`FileSystem` - Publish by copying files to a specified folder.</span></span>

### <a name="specifying-the-build-configuration-and-platform"></a><span data-ttu-id="b5944-152">指定生成配置和平台</span><span class="sxs-lookup"><span data-stu-id="b5944-152">Specifying the build configuration and platform</span></span>

<span data-ttu-id="b5944-153">必须在 Visual Studio 或命令行中设置生成配置和平台。</span><span class="sxs-lookup"><span data-stu-id="b5944-153">The build configuration and platform must be set in Visual Studio or on the command line.</span></span> <span data-ttu-id="b5944-154">发布配置文件包含名为 `LastUsedBuildConfiguration` 和 `LastUsedPlatform`的属性，但您不能设置这些属性以确定项目的生成方式。</span><span class="sxs-lookup"><span data-stu-id="b5944-154">The publish profiles include properties that are named `LastUsedBuildConfiguration` and `LastUsedPlatform`, but you can't set these properties in order to determine how the project is built.</span></span> <span data-ttu-id="b5944-155">有关详细信息，请参阅 Sayed Hashimi 的博客上的[MSBuild：如何设置配置属性](http://sedodream.com/2012/10/27/MSBuildHowToSetTheConfigurationProperty.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b5944-155">For more information, see [MSBuild: how to set the configuration property](http://sedodream.com/2012/10/27/MSBuildHowToSetTheConfigurationProperty.aspx) on Sayed Hashimi's blog.</span></span>

## <a name="deploy-to-staging"></a><span data-ttu-id="b5944-156">部署到过渡环境</span><span class="sxs-lookup"><span data-stu-id="b5944-156">Deploy to staging</span></span>

<span data-ttu-id="b5944-157">若要部署到 Azure，必须将密码添加到命令行。</span><span class="sxs-lookup"><span data-stu-id="b5944-157">To deploy to Azure, you must add the password to the command line.</span></span> <span data-ttu-id="b5944-158">如果你在 Visual Studio 中的发布配置文件中保存了密码，则该密码将以加密形式存储在 *.pubxml*文件中。</span><span class="sxs-lookup"><span data-stu-id="b5944-158">If you saved the password in the publish profile in Visual Studio, it was stored in encrypted form in the your *.pubxml.user* file.</span></span> <span data-ttu-id="b5944-159">当你执行命令行部署时，MSBuild 不会访问该文件，因此你必须在命令行参数中传递密码。</span><span class="sxs-lookup"><span data-stu-id="b5944-159">That file is not accessed by MSBuild when you do a command line deployment, so you have to pass in the password in a command line parameter.</span></span>

1. <span data-ttu-id="b5944-160">从之前为暂存网站下载的 *.publishsettings*文件中复制所需的密码。</span><span class="sxs-lookup"><span data-stu-id="b5944-160">Copy the password that you need from the *.publishsettings* file that you downloaded earlier for the staging web site.</span></span> <span data-ttu-id="b5944-161">密码是 Web 部署 `publishProfile` 元素的 `userPWD` 属性的值。</span><span class="sxs-lookup"><span data-stu-id="b5944-161">The password is the value of the `userPWD` attribute for the Web Deploy `publishProfile` element.</span></span>

    ![Web 部署密码](command-line-deployment/_static/image5.png)
2. <span data-ttu-id="b5944-163">在 Windows 8 "开始" 页上，搜索 "**开发人员命令提示**"，然后单击图标以打开命令提示符。</span><span class="sxs-lookup"><span data-stu-id="b5944-163">In the Windows 8 Start page, search for **Developer Command Prompt for VS2012**, and click the icon to open the command prompt.</span></span> <span data-ttu-id="b5944-164">（此时无需在管理员的情况下将其打开，因为你不会部署到本地计算机上的 IIS。）</span><span class="sxs-lookup"><span data-stu-id="b5944-164">(You don't have to open it as administrator this time because you aren't deploying to IIS on the local computer.)</span></span>
3. <span data-ttu-id="b5944-165">在命令提示符下输入以下命令，将解决方案文件的路径替换为您的解决方案文件的路径，并将密码替换为您的密码：</span><span class="sxs-lookup"><span data-stu-id="b5944-165">Enter the following command at the command prompt, replacing the path to the solution file with the path to your solution file and the password with your password:</span></span>

    [!code-console[Main](command-line-deployment/samples/sample6.cmd)]

    <span data-ttu-id="b5944-166">请注意，此命令行包含额外参数： `/p:AllowUntrustedCertificate=true`。</span><span class="sxs-lookup"><span data-stu-id="b5944-166">Notice that this command line includes an extra parameter: `/p:AllowUntrustedCertificate=true`.</span></span> <span data-ttu-id="b5944-167">编写本教程时，必须在从命令行发布到 Azure 时设置 `AllowUntrustedCertificate` 属性。</span><span class="sxs-lookup"><span data-stu-id="b5944-167">As this tutorial is being written, the `AllowUntrustedCertificate` property must be set when you publish to Azure from the command line.</span></span> <span data-ttu-id="b5944-168">发布此 bug 的修补程序后，你不需要该参数。</span><span class="sxs-lookup"><span data-stu-id="b5944-168">When the fix for this bug is released, you won't need that parameter.</span></span>
4. <span data-ttu-id="b5944-169">打开浏览器并中转到过渡站点的 URL，然后单击 "**关于**" 页以验证部署是否成功。</span><span class="sxs-lookup"><span data-stu-id="b5944-169">Open a browser and go to the URL of your staging site, and then click the **About** page to verify that the deployment was successful.</span></span>

    <span data-ttu-id="b5944-170">正如你之前在测试环境中看到的那样，你可能需要创建一些学生，才能在 "**关于**" 页上查看统计信息。</span><span class="sxs-lookup"><span data-stu-id="b5944-170">As you saw earlier for the test environment, you might have to create some students to see statistics on the **About** page.</span></span>

## <a name="deploy-to-production"></a><span data-ttu-id="b5944-171">部署到生产环境</span><span class="sxs-lookup"><span data-stu-id="b5944-171">Deploy to production</span></span>

<span data-ttu-id="b5944-172">部署到生产环境的过程类似于过渡过程。</span><span class="sxs-lookup"><span data-stu-id="b5944-172">The process for deploying to production is similar to the process for staging.</span></span>

1. <span data-ttu-id="b5944-173">从之前为生产网站下载的 *.publishsettings*文件中复制所需的密码。</span><span class="sxs-lookup"><span data-stu-id="b5944-173">Copy the password that you need from the *.publishsettings* file that you downloaded earlier for the production web site.</span></span>
2. <span data-ttu-id="b5944-174">打开**VS2012 开发人员命令提示**。</span><span class="sxs-lookup"><span data-stu-id="b5944-174">Open **Developer Command Prompt for VS2012**.</span></span>
3. <span data-ttu-id="b5944-175">在命令提示符下输入以下命令，将解决方案文件的路径替换为您的解决方案文件的路径，并将密码替换为您的密码：</span><span class="sxs-lookup"><span data-stu-id="b5944-175">Enter the following command at the command prompt, replacing the path to the solution file with the path to your solution file and the password with your password:</span></span>

    [!code-console[Main](command-line-deployment/samples/sample7.cmd)]

    <span data-ttu-id="b5944-176">对于实际的生产站点，如果也存在数据库更改，则通常会在部署之前将*应用\_脱机*文件复制到站点，并在部署成功后将其删除。</span><span class="sxs-lookup"><span data-stu-id="b5944-176">For a real production site, if there was also a database change, you would typically copy the *app\_offline.htm* file to the site before deployment and delete it after successful deployment.</span></span>
4. <span data-ttu-id="b5944-177">打开浏览器并中转到过渡站点的 URL，然后单击 "**关于**" 页以验证部署是否成功。</span><span class="sxs-lookup"><span data-stu-id="b5944-177">Open a browser and go to the URL of your staging site, and then click the **About** page to verify that the deployment was successful.</span></span>

## <a name="summary"></a><span data-ttu-id="b5944-178">摘要</span><span class="sxs-lookup"><span data-stu-id="b5944-178">Summary</span></span>

<span data-ttu-id="b5944-179">现在，你已使用命令行部署了一个应用程序更新。</span><span class="sxs-lookup"><span data-stu-id="b5944-179">You have now deployed an application update by using the command line.</span></span>

![测试环境中的 "关于" 页](command-line-deployment/_static/image6.png)

<span data-ttu-id="b5944-181">在下一教程中，你将看到有关如何扩展 web 发布管道的示例。</span><span class="sxs-lookup"><span data-stu-id="b5944-181">In the next tutorial, you will see an example of how to extend the web publish pipeline.</span></span> <span data-ttu-id="b5944-182">此示例将演示如何部署项目中未包含的文件。</span><span class="sxs-lookup"><span data-stu-id="b5944-182">The example will show you how to deploy files that are not included in the project.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b5944-183">[上一页](deploying-a-database-update.md)
> [下一页](deploying-extra-files.md)</span><span class="sxs-lookup"><span data-stu-id="b5944-183">[Previous](deploying-a-database-update.md)
[Next](deploying-extra-files.md)</span></span>
