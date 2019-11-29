---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything
title: 自动执行所有操作（通过 Azure 构建实际的云应用） |Microsoft Docs
author: MikeWasson
description: 使用 Azure 电子书构建真实的云应用基于 Scott Guthrie 开发的演示文稿。 它介绍了13种模式和实践，
ms.author: riande
ms.date: 06/12/2014
ms.assetid: ba6e6baa-9b9f-471f-b39d-b007a3addadc
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything
msc.type: authoredcontent
ms.openlocfilehash: d5c8190d0b0c91bf9e42f6ef03adc5b07a65359a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74582892"
---
# <a name="automate-everything-building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="fceb0-104">自动执行所有操作（通过 Azure 构建实际的云应用）</span><span class="sxs-lookup"><span data-stu-id="fceb0-104">Automate Everything (Building Real-World Cloud Apps with Azure)</span></span>

<span data-ttu-id="fceb0-105">作者： [Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson]((https://twitter.com/RickAndMSFT))， [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="fceb0-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="fceb0-106">[下载 Fix It 项目](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="fceb0-106">[Download Fix It Project](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) or [Download E-book](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span></span>

> <span data-ttu-id="fceb0-107">**使用 Azure 电子书构建真实的云应用**基于 Scott Guthrie 开发的演示文稿。</span><span class="sxs-lookup"><span data-stu-id="fceb0-107">The **Building Real World Cloud Apps with Azure** e-book is based on a presentation developed by Scott Guthrie.</span></span> <span data-ttu-id="fceb0-108">它介绍了可帮助你成功开发云的 web 应用的13种模式和实践。</span><span class="sxs-lookup"><span data-stu-id="fceb0-108">It explains 13 patterns and practices that can help you be successful developing web apps for the cloud.</span></span> <span data-ttu-id="fceb0-109">有关电子书的简介，请参阅[第一章](introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="fceb0-109">For an introduction to the e-book, see [the first chapter](introduction.md).</span></span>

<span data-ttu-id="fceb0-110">我们所要做的前三种模式实际上适用于任何软件开发项目，尤其是云项目。</span><span class="sxs-lookup"><span data-stu-id="fceb0-110">The first three patterns we'll look at actually apply to any software development project, but especially to cloud projects.</span></span> <span data-ttu-id="fceb0-111">此模式与自动执行开发任务有关。</span><span class="sxs-lookup"><span data-stu-id="fceb0-111">This pattern is about automating development tasks.</span></span> <span data-ttu-id="fceb0-112">这是一个重要的主题，因为手动过程速度慢且容易出错;尽可能多地自动执行这些功能可帮助设置快速、可靠和敏捷的工作流。</span><span class="sxs-lookup"><span data-stu-id="fceb0-112">It's an important topic because manual processes are slow and error-prone; automating as many of them as possible helps set up a fast, reliable, and agile workflow.</span></span> <span data-ttu-id="fceb0-113">这对于云开发而言是唯一重要的，因为你可以在本地环境中轻松地自动执行许多难于或无法自动执行的任务。</span><span class="sxs-lookup"><span data-stu-id="fceb0-113">It's uniquely important for cloud development because you can easily automate many tasks that are difficult or impossible to automate in an on-premises environment.</span></span> <span data-ttu-id="fceb0-114">例如，可以设置整个测试环境，包括新的 web 服务器和后端 Vm、数据库、blob 存储（文件存储）、队列等。</span><span class="sxs-lookup"><span data-stu-id="fceb0-114">For example, you can set up whole test environments including new web server and back-end VMs, databases, blob storage (file storage), queues, etc.</span></span>

## <a name="devops-workflow"></a><span data-ttu-id="fceb0-115">DevOps 工作流</span><span class="sxs-lookup"><span data-stu-id="fceb0-115">DevOps Workflow</span></span>

<span data-ttu-id="fceb0-116">您越来越多地听到了 "DevOps" 一词。</span><span class="sxs-lookup"><span data-stu-id="fceb0-116">Increasingly you hear the term "DevOps."</span></span> <span data-ttu-id="fceb0-117">这一术语是在识别中开发的，你必须集成开发和操作任务才能有效地开发软件。</span><span class="sxs-lookup"><span data-stu-id="fceb0-117">The term developed out of a recognition that you have to integrate development and operations tasks in order to develop software efficiently.</span></span> <span data-ttu-id="fceb0-118">要启用的工作流类型为：你可以在其中开发应用、部署应用、从产品的生产使用情况中进行更改、根据你了解的内容进行更改，以及快速可靠地重复周期。</span><span class="sxs-lookup"><span data-stu-id="fceb0-118">The kind of workflow you want to enable is one in which you can develop an app, deploy it, learn from production usage of it, change it in response to what you've learned, and repeat the cycle quickly and reliably.</span></span>

<span data-ttu-id="fceb0-119">一些成功的云开发团队每天将多次部署到实时环境。</span><span class="sxs-lookup"><span data-stu-id="fceb0-119">Some successful cloud development teams deploy multiple times a day to a live environment.</span></span> <span data-ttu-id="fceb0-120">每2-3 个月使用 Azure 团队部署一个主要更新，但现在它每2-3 天发布少量更新，每2-3 周发布一次主发布。</span><span class="sxs-lookup"><span data-stu-id="fceb0-120">The Azure team used to deploy a major update every 2-3 months, but now it releases minor updates every 2-3 days and major releases every 2-3 weeks.</span></span> <span data-ttu-id="fceb0-121">进入该节奏确实有助于您迅速响应客户反馈。</span><span class="sxs-lookup"><span data-stu-id="fceb0-121">Getting into that cadence really helps you be responsive to customer feedback.</span></span>

<span data-ttu-id="fceb0-122">要执行此操作，必须启用可重复的、可靠的、可预测的开发和部署周期，并缩短周期时间。</span><span class="sxs-lookup"><span data-stu-id="fceb0-122">In order to do that, you have to enable a development and deployment cycle that is repeatable, reliable, predictable, and has low cycle time.</span></span>

![DevOps 工作流](automate-everything/_static/image1.png)

<span data-ttu-id="fceb0-124">换句话说，您对某个功能的想法以及客户使用该功能并提供反馈的时间段必须尽可能简短。</span><span class="sxs-lookup"><span data-stu-id="fceb0-124">In other words, the period of time between when you have an idea for a feature and when the customers are using it and providing feedback must be as short as possible.</span></span> <span data-ttu-id="fceb0-125">前三种模式（自动执行所有操作、源代码管理和持续集成和交付）都涉及到为了启用这种过程而建议使用的最佳实践。</span><span class="sxs-lookup"><span data-stu-id="fceb0-125">The first three patterns – automate everything, source control, and continuous integration and delivery -- are all about best practices that we recommend in order to enable that kind of process.</span></span>

## <a name="azure-management-scripts"></a><span data-ttu-id="fceb0-126">Azure 管理脚本</span><span class="sxs-lookup"><span data-stu-id="fceb0-126">Azure management scripts</span></span>

<span data-ttu-id="fceb0-127">[本电子书简介介绍](introduction.md)了基于 web 的控制台，即 Azure 管理门户。</span><span class="sxs-lookup"><span data-stu-id="fceb0-127">In the [introduction to this e-book](introduction.md), you saw the web-based console, the Azure Management Portal.</span></span> <span data-ttu-id="fceb0-128">使用管理门户可以监视和管理已部署在 Azure 上的所有资源。</span><span class="sxs-lookup"><span data-stu-id="fceb0-128">The management portal enables you to monitor and manage all of the resources that you have deployed on Azure.</span></span> <span data-ttu-id="fceb0-129">这是创建和删除服务（如 web 应用和 Vm）、配置这些服务、监视服务操作等的简单方法。</span><span class="sxs-lookup"><span data-stu-id="fceb0-129">It's an easy way to create and delete services such as web apps and VMs, configure those services, monitor service operation, and so forth.</span></span> <span data-ttu-id="fceb0-130">这是一个很好的工具，但使用它是一个手动过程。</span><span class="sxs-lookup"><span data-stu-id="fceb0-130">It's a great tool, but using it is a manual process.</span></span> <span data-ttu-id="fceb0-131">如果你打算开发任何规模的生产应用程序，尤其是在团队环境中，建议你通过门户 UI 来学习和探索 Azure，然后自动执行要重复执行的过程。</span><span class="sxs-lookup"><span data-stu-id="fceb0-131">If you're going to develop a production application of any size, and especially in a team environment, we recommend that you go through the portal UI in order to learn and explore Azure, and then automate the processes that you'll be doing repetitively.</span></span>

<span data-ttu-id="fceb0-132">几乎可以在管理门户或 Visual Studio 中手动完成的所有操作也可以通过调用 REST 管理 API 来完成。</span><span class="sxs-lookup"><span data-stu-id="fceb0-132">Nearly everything that you can do manually in the management portal or from Visual Studio can also be done by calling the REST management API.</span></span> <span data-ttu-id="fceb0-133">可以使用[Windows PowerShell](https://msdn.microsoft.com/library/windowsazure/jj156055.aspx)编写脚本，也可以使用开源框架（如[Chef](http://www.opscode.com/chef/)或[Puppet](http://puppetlabs.com/puppet/what-is-puppet)）。</span><span class="sxs-lookup"><span data-stu-id="fceb0-133">You can write scripts using [Windows PowerShell](https://msdn.microsoft.com/library/windowsazure/jj156055.aspx), or you can use an open source framework such as [Chef](http://www.opscode.com/chef/) or [Puppet](http://puppetlabs.com/puppet/what-is-puppet).</span></span> <span data-ttu-id="fceb0-134">你还可以在 Mac 或 Linux 环境中使用 Bash 命令行工具。</span><span class="sxs-lookup"><span data-stu-id="fceb0-134">You can also use the Bash command-line tool in a Mac or Linux environment.</span></span> <span data-ttu-id="fceb0-135">Azure 已为所有这些不同的环境编写 Api 脚本，并具有[.net 管理 API](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx) ，以防你想要编写代码而不是脚本。</span><span class="sxs-lookup"><span data-stu-id="fceb0-135">Azure has scripting APIs for all those different environments, and it has a [.NET management API](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx) in case you want to write code instead of script.</span></span>

<span data-ttu-id="fceb0-136">对于 Fix It 应用，我们创建了一些 Windows PowerShell 脚本，这些脚本会自动执行创建测试环境的过程，并将项目部署到该环境，我们将查看这些脚本的一些内容。</span><span class="sxs-lookup"><span data-stu-id="fceb0-136">For the Fix It app we've created some Windows PowerShell scripts that automate the processes of creating a test environment and deploying the project to that environment, and we'll review some of the contents of those scripts.</span></span>

## <a name="environment-creation-script"></a><span data-ttu-id="fceb0-137">环境创建脚本</span><span class="sxs-lookup"><span data-stu-id="fceb0-137">Environment creation script</span></span>

<span data-ttu-id="fceb0-138">我们将查看的第一个脚本名为*New-AzureWebsiteEnv*。</span><span class="sxs-lookup"><span data-stu-id="fceb0-138">The first script we'll look at is named *New-AzureWebsiteEnv.ps1*.</span></span> <span data-ttu-id="fceb0-139">它创建一个 Azure 环境，你可以将 Fix It 应用部署到该环境以进行测试。</span><span class="sxs-lookup"><span data-stu-id="fceb0-139">It creates an Azure environment that you can deploy the Fix It app to for testing.</span></span> <span data-ttu-id="fceb0-140">此脚本执行的主要任务如下：</span><span class="sxs-lookup"><span data-stu-id="fceb0-140">The main tasks that this script performs are the following:</span></span>

- <span data-ttu-id="fceb0-141">创建 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="fceb0-141">Create a web app.</span></span>
- <span data-ttu-id="fceb0-142">创建存储帐户。</span><span class="sxs-lookup"><span data-stu-id="fceb0-142">Create a storage account.</span></span> <span data-ttu-id="fceb0-143">（Blob 和队列需要，如后面的章节中所示。）</span><span class="sxs-lookup"><span data-stu-id="fceb0-143">(Required for blobs and queues, as you'll see in later chapters.)</span></span>
- <span data-ttu-id="fceb0-144">创建 SQL 数据库服务器和两个数据库：应用程序数据库和成员资格数据库。</span><span class="sxs-lookup"><span data-stu-id="fceb0-144">Create a SQL Database server and two databases: an application database, and a membership database.</span></span>
- <span data-ttu-id="fceb0-145">在 Azure 中存储用于访问存储帐户和数据库的设置。</span><span class="sxs-lookup"><span data-stu-id="fceb0-145">Store settings in Azure that the app will use to access the storage account and databases.</span></span>
- <span data-ttu-id="fceb0-146">创建将用于自动部署的设置文件。</span><span class="sxs-lookup"><span data-stu-id="fceb0-146">Create settings files that will be used to automate deployment.</span></span>

### <a name="run-the-script"></a><span data-ttu-id="fceb0-147">运行脚本</span><span class="sxs-lookup"><span data-stu-id="fceb0-147">Run the script</span></span>

> [!NOTE]
> <span data-ttu-id="fceb0-148">本章的此部分将显示脚本的示例，以及为运行脚本而输入的命令。</span><span class="sxs-lookup"><span data-stu-id="fceb0-148">This part of the chapter shows examples of scripts and the commands that you enter in order to run them.</span></span> <span data-ttu-id="fceb0-149">这是一个演示，不提供运行脚本所需的知识。</span><span class="sxs-lookup"><span data-stu-id="fceb0-149">This a demo and doesn't provide everything you need to know in order to run the scripts.</span></span> <span data-ttu-id="fceb0-150">有关分步操作说明，请参阅[附录： Fix It 示例应用程序](the-fix-it-sample-application.md#deploybase)。</span><span class="sxs-lookup"><span data-stu-id="fceb0-150">For step-by-step how-to-do-it instructions, see [Appendix: The Fix It Sample Application](the-fix-it-sample-application.md#deploybase).</span></span>

<span data-ttu-id="fceb0-151">要运行管理 Azure 服务的 PowerShell 脚本，你必须安装 Azure PowerShell 控制台并将其配置为使用 Azure 订阅。</span><span class="sxs-lookup"><span data-stu-id="fceb0-151">To run a PowerShell script that manages Azure services you have to install the Azure PowerShell console and configure it to work with your Azure subscription.</span></span> <span data-ttu-id="fceb0-152">设置后，可以使用以下命令运行 Fix It 环境创建脚本：</span><span class="sxs-lookup"><span data-stu-id="fceb0-152">Once you're set up, you can run the Fix It environment creation script with a command like this one:</span></span>

`.\New-AzureWebsiteEnv.ps1 -Name <websitename> -SqlDatabasePassword <password>`

<span data-ttu-id="fceb0-153">`Name` 参数指定在创建数据库和存储帐户时要使用的名称，而 `SqlDatabasePassword` 参数指定将为 SQL 数据库创建的管理员帐户的密码。</span><span class="sxs-lookup"><span data-stu-id="fceb0-153">The `Name` parameter specifies the name to be used when creating the database and storage accounts, and the `SqlDatabasePassword` parameter specifies the password for the admin account that will be created for SQL Database.</span></span> <span data-ttu-id="fceb0-154">您可以使用其他参数，以后我们将对此进行介绍。</span><span class="sxs-lookup"><span data-stu-id="fceb0-154">There are other parameters you can use that we'll look at later.</span></span>

![PowerShell 窗口](automate-everything/_static/image2.png)

<span data-ttu-id="fceb0-156">脚本完成后，可以在管理门户中看到创建的内容。</span><span class="sxs-lookup"><span data-stu-id="fceb0-156">After the script finishes you can see in the management portal what was created.</span></span> <span data-ttu-id="fceb0-157">你会发现两个数据库：</span><span class="sxs-lookup"><span data-stu-id="fceb0-157">You'll find two databases:</span></span>

![数据库](automate-everything/_static/image3.png)

<span data-ttu-id="fceb0-159">存储帐户：</span><span class="sxs-lookup"><span data-stu-id="fceb0-159">A storage account:</span></span>

![存储帐户](automate-everything/_static/image4.png)

<span data-ttu-id="fceb0-161">和 web 应用：</span><span class="sxs-lookup"><span data-stu-id="fceb0-161">And a web app:</span></span>

![网站](automate-everything/_static/image5.png)

<span data-ttu-id="fceb0-163">在 web 应用的 "**配置**" 选项卡上，可以看到它已为 Fix it 应用程序设置了存储帐户设置和 SQL 数据库连接字符串。</span><span class="sxs-lookup"><span data-stu-id="fceb0-163">On the **Configure** tab for the web app, you can see that it has the storage account settings and SQL database connection strings set up for the Fix It app.</span></span>

![appSettings 和 connectionStrings](automate-everything/_static/image6.png)

<span data-ttu-id="fceb0-165">*自动化*文件夹现在还包含一个 *&lt;websitename&gt;.pubxml*文件。</span><span class="sxs-lookup"><span data-stu-id="fceb0-165">The *Automation* folder now also contains a *&lt;websitename&gt;.pubxml* file.</span></span> <span data-ttu-id="fceb0-166">此文件存储 MSBuild 将用于将应用程序部署到刚刚创建的 Azure 环境的设置。</span><span class="sxs-lookup"><span data-stu-id="fceb0-166">This file stores settings that MSBuild will use to deploy the application to the Azure environment that was just created.</span></span> <span data-ttu-id="fceb0-167">例如：</span><span class="sxs-lookup"><span data-stu-id="fceb0-167">For example:</span></span>

[!code-xml[Main](automate-everything/samples/sample1.xml)]

<span data-ttu-id="fceb0-168">如您所见，该脚本创建了一个完整的测试环境，整个过程大约在90秒内完成。</span><span class="sxs-lookup"><span data-stu-id="fceb0-168">As you can see, the script has created a complete test environment, and the whole process is done in about 90 seconds.</span></span>

<span data-ttu-id="fceb0-169">如果你的团队中的其他人想要创建测试环境，则可以直接运行该脚本。</span><span class="sxs-lookup"><span data-stu-id="fceb0-169">If someone else on your team wants to create a test environment, they can just run the script.</span></span> <span data-ttu-id="fceb0-170">它不仅快速，而且还可以确信他们使用的环境与你使用的环境相同。</span><span class="sxs-lookup"><span data-stu-id="fceb0-170">Not only is it fast, but also they can be confident that they are using an environment identical to the one you're using.</span></span> <span data-ttu-id="fceb0-171">如果每个人都使用管理门户 UI 手动设置，就不能完全相信这一点。</span><span class="sxs-lookup"><span data-stu-id="fceb0-171">You couldn't be quite as confident of that if everyone was setting things up manually by using the management portal UI.</span></span>

### <a name="a-look-at-the-scripts"></a><span data-ttu-id="fceb0-172">查看脚本</span><span class="sxs-lookup"><span data-stu-id="fceb0-172">A look at the scripts</span></span>

<span data-ttu-id="fceb0-173">实际上有三个用于执行此操作的脚本。</span><span class="sxs-lookup"><span data-stu-id="fceb0-173">There are actually three scripts that do this work.</span></span> <span data-ttu-id="fceb0-174">从命令行调用一个命令，它会自动使用其他两个任务来执行某些任务：</span><span class="sxs-lookup"><span data-stu-id="fceb0-174">You call one from the command line and it automatically uses the other two to do some of the tasks:</span></span>

- <span data-ttu-id="fceb0-175">*New-AzureWebSiteEnv*是主要脚本。</span><span class="sxs-lookup"><span data-stu-id="fceb0-175">*New-AzureWebSiteEnv.ps1* is the main script.</span></span>

    - <span data-ttu-id="fceb0-176">*New-AzureStorage*创建存储帐户。</span><span class="sxs-lookup"><span data-stu-id="fceb0-176">*New-AzureStorage.ps1* creates the storage account.</span></span>
    - <span data-ttu-id="fceb0-177">*New-AzureSql*将创建数据库。</span><span class="sxs-lookup"><span data-stu-id="fceb0-177">*New-AzureSql.ps1* creates the databases.</span></span>

### <a name="parameters-in-the-main-script"></a><span data-ttu-id="fceb0-178">主脚本中的参数</span><span class="sxs-lookup"><span data-stu-id="fceb0-178">Parameters in the main script</span></span>

<span data-ttu-id="fceb0-179">主脚本*New-AzureWebSiteEnv*定义了多个参数：</span><span class="sxs-lookup"><span data-stu-id="fceb0-179">The main script, *New-AzureWebSiteEnv.ps1*, defines several parameters:</span></span>

[!code-powershell[Main](automate-everything/samples/sample2.ps1)]

<span data-ttu-id="fceb0-180">需要两个参数：</span><span class="sxs-lookup"><span data-stu-id="fceb0-180">Two parameters are required:</span></span>

- <span data-ttu-id="fceb0-181">此脚本创建的 web 应用的名称。</span><span class="sxs-lookup"><span data-stu-id="fceb0-181">The name of the web app that the script creates.</span></span> <span data-ttu-id="fceb0-182">（这也用于 URL： `<name>.azurewebsites.net`。）</span><span class="sxs-lookup"><span data-stu-id="fceb0-182">(This is also used for the URL: `<name>.azurewebsites.net`.)</span></span>
- <span data-ttu-id="fceb0-183">脚本创建的数据库服务器的新管理用户的密码。</span><span class="sxs-lookup"><span data-stu-id="fceb0-183">The password for the new administrative user of the database server that the script creates.</span></span>

<span data-ttu-id="fceb0-184">可选参数可用于指定数据中心位置（默认为 "美国西部"）、数据库服务器管理员名称（默认为 "dbuser"）和数据库服务器的防火墙规则。</span><span class="sxs-lookup"><span data-stu-id="fceb0-184">Optional parameters enable you to specify the data center location (defaults to "West US"), database server administrator name (defaults to "dbuser"), and a firewall rule for the database server.</span></span>

### <a name="create-the-web-app"></a><span data-ttu-id="fceb0-185">创建 Web 应用</span><span class="sxs-lookup"><span data-stu-id="fceb0-185">Create the web app</span></span>

<span data-ttu-id="fceb0-186">脚本的第一件事就是通过调用 `New-AzureWebsite` cmdlet 创建 web 应用，并向其传递 web 应用名称和位置参数值：</span><span class="sxs-lookup"><span data-stu-id="fceb0-186">The first thing the script does is create the web app by calling the `New-AzureWebsite` cmdlet, passing in to it the web app name and location parameter values:</span></span>

[!code-powershell[Main](automate-everything/samples/sample3.ps1?highlight=2)]

### <a name="create-the-storage-account"></a><span data-ttu-id="fceb0-187">创建存储帐户</span><span class="sxs-lookup"><span data-stu-id="fceb0-187">Create the storage account</span></span>

<span data-ttu-id="fceb0-188">然后，主脚本运行*New-AzureStorage*脚本，并为存储帐户名称指定 " *&lt;websitename&gt;* 存储"，并为 web 应用指定相同的数据中心位置。</span><span class="sxs-lookup"><span data-stu-id="fceb0-188">Then the main script runs the *New-AzureStorage.ps1* script, specifying "*&lt;websitename&gt;* storage" for the storage account name, and the same data center location as the web app.</span></span>

[!code-powershell[Main](automate-everything/samples/sample4.ps1?highlight=3)]

<span data-ttu-id="fceb0-189">*New-AzureStorage*调用 `New-AzureStorageAccount` cmdlet 来创建存储帐户，并返回帐户名称和访问密钥值。</span><span class="sxs-lookup"><span data-stu-id="fceb0-189">*New-AzureStorage.ps1* calls the `New-AzureStorageAccount` cmdlet to create the storage account, and it returns the account name and access key values.</span></span> <span data-ttu-id="fceb0-190">应用程序需要这些值才能访问存储帐户中的 blob 和队列。</span><span class="sxs-lookup"><span data-stu-id="fceb0-190">The application will need these values in order to access the blobs and queues in the storage account.</span></span>

[!code-powershell[Main](automate-everything/samples/sample5.ps1?highlight=2)]

<span data-ttu-id="fceb0-191">您可能不需要始终创建新的存储帐户;可以通过添加参数来增强脚本，此参数可选择指示使用现有的存储帐户。</span><span class="sxs-lookup"><span data-stu-id="fceb0-191">You might not always want to create a new storage account; you could enhance the script by adding a parameter that optionally directs it to use an existing storage account.</span></span>

### <a name="create-the-databases"></a><span data-ttu-id="fceb0-192">创建数据库</span><span class="sxs-lookup"><span data-stu-id="fceb0-192">Create the databases</span></span>

<span data-ttu-id="fceb0-193">然后，主脚本在设置默认数据库和防火墙规则名称后运行数据库创建脚本*New-AzureSql*：</span><span class="sxs-lookup"><span data-stu-id="fceb0-193">The main script then runs the database creation script, *New-AzureSql.ps1*, after setting up default database and firewall rule names:</span></span>

[!code-powershell[Main](automate-everything/samples/sample6.ps1)]

[!code-powershell[Main](automate-everything/samples/sample7.ps1?highlight=2)]

<span data-ttu-id="fceb0-194">数据库创建脚本检索 dev 计算机的 IP 地址并设置防火墙规则，以便 dev 计算机可以连接到服务器并对其进行管理。</span><span class="sxs-lookup"><span data-stu-id="fceb0-194">The database creation script retrieves the dev machine's IP address and sets a firewall rule so the dev machine can connect to and manage the server.</span></span> <span data-ttu-id="fceb0-195">然后，数据库创建脚本完成多个步骤以设置数据库：</span><span class="sxs-lookup"><span data-stu-id="fceb0-195">The database creation script then goes through several steps to set up the databases:</span></span>

- <span data-ttu-id="fceb0-196">使用 `New-AzureSqlDatabaseServer` cmdlet 创建服务器。</span><span class="sxs-lookup"><span data-stu-id="fceb0-196">Creates the server by using the `New-AzureSqlDatabaseServer` cmdlet.</span></span>

    [!code-powershell[Main](automate-everything/samples/sample8.ps1?highlight=1)]
- <span data-ttu-id="fceb0-197">创建防火墙规则，使开发计算机能够管理服务器并使 web 应用程序能够连接到该服务器。</span><span class="sxs-lookup"><span data-stu-id="fceb0-197">Creates firewall rules to enable the dev machine to manage the server and to enable the web app to connect to it.</span></span> 

    [!code-powershell[Main](automate-everything/samples/sample9.ps1?highlight=3,5)]
- <span data-ttu-id="fceb0-198">使用 `New-AzureSqlDatabaseServerContext` cmdlet 创建包括服务器名称和凭据的数据库上下文。</span><span class="sxs-lookup"><span data-stu-id="fceb0-198">Creates a database context that includes the server name and credentials, by using the `New-AzureSqlDatabaseServerContext` cmdlet.</span></span>

    [!code-powershell[Main](automate-everything/samples/sample10.ps1?highlight=4)]

    <span data-ttu-id="fceb0-199">`New-PSCredentialFromPlainText` 是脚本中的一个函数，该函数调用 `ConvertTo-SecureString` cmdlet 来加密密码并返回 `PSCredential` 对象，这与 `Get-Credential` cmdlet 返回的类型相同。</span><span class="sxs-lookup"><span data-stu-id="fceb0-199">`New-PSCredentialFromPlainText` is a function in the script that calls the `ConvertTo-SecureString` cmdlet to encrypt the password and returns a `PSCredential` object, the same type that the `Get-Credential` cmdlet returns.</span></span>
- <span data-ttu-id="fceb0-200">使用 `New-AzureSqlDatabase` cmdlet 创建应用程序数据库和成员资格数据库。</span><span class="sxs-lookup"><span data-stu-id="fceb0-200">Creates the application database and the membership database by using the `New-AzureSqlDatabase` cmdlet.</span></span>

    [!code-powershell[Main](automate-everything/samples/sample11.ps1?highlight=2,5)]
- <span data-ttu-id="fceb0-201">调用本地定义的函数以创建每个数据库的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="fceb0-201">Calls a locally defined function to create a connection string for each database.</span></span> <span data-ttu-id="fceb0-202">应用程序将使用这些连接字符串访问数据库。</span><span class="sxs-lookup"><span data-stu-id="fceb0-202">The application will use these connection strings to access the databases.</span></span> 

    [!code-powershell[Main](automate-everything/samples/sample12.ps1?highlight=1-2)]

    <span data-ttu-id="fceb0-203">SQLAzureDatabaseConnectionString 是在脚本中定义的一个函数，该函数从提供给它的参数值创建连接字符串。</span><span class="sxs-lookup"><span data-stu-id="fceb0-203">Get-SQLAzureDatabaseConnectionString is a function defined in the script that creates the connection string from the parameter values supplied to it.</span></span>

    [!code-powershell[Main](automate-everything/samples/sample13.ps1?highlight=1)]
- <span data-ttu-id="fceb0-204">返回一个哈希表，其中包含数据库服务器名称和连接字符串。</span><span class="sxs-lookup"><span data-stu-id="fceb0-204">Returns a hash table with the database server name and the connection strings.</span></span>

    [!code-powershell[Main](automate-everything/samples/sample14.ps1)]

<span data-ttu-id="fceb0-205">Fix It 应用使用单独的成员身份和应用程序数据库。</span><span class="sxs-lookup"><span data-stu-id="fceb0-205">The Fix It app uses separate membership and application databases.</span></span> <span data-ttu-id="fceb0-206">还可以将成员资格和应用程序数据放在单个数据库中。</span><span class="sxs-lookup"><span data-stu-id="fceb0-206">It's also possible to put both membership and application data in a single database.</span></span>

### <a name="store-app-settings-and-connection-strings"></a><span data-ttu-id="fceb0-207">存储应用设置和连接字符串</span><span class="sxs-lookup"><span data-stu-id="fceb0-207">Store app settings and connection strings</span></span>

<span data-ttu-id="fceb0-208">Azure 提供了一项功能，使你能够存储设置和连接字符串，以便在尝试读取 web.config 文件中的 `appSettings` 或 `connectionStrings` 集合时自动覆盖返回到应用程序的内容。</span><span class="sxs-lookup"><span data-stu-id="fceb0-208">Azure has a feature that enables you to store settings and connection strings that automatically override what is returned to the application when it tries to read the `appSettings` or `connectionStrings` collections in the Web.config file.</span></span> <span data-ttu-id="fceb0-209">这是在部署时应用 web.config[转换](../../../../web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations.md)的替代方法。</span><span class="sxs-lookup"><span data-stu-id="fceb0-209">This is an alternative to applying [Web.config transformations](../../../../web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations.md) when you deploy.</span></span> <span data-ttu-id="fceb0-210">有关详细信息，请参阅本电子书后面的在[Azure 中存储敏感数据](source-control.md#appsettings)。</span><span class="sxs-lookup"><span data-stu-id="fceb0-210">For more information, see [Store sensitive data in Azure](source-control.md#appsettings) later in this e-book.</span></span>

<span data-ttu-id="fceb0-211">环境创建脚本将所有 `appSettings` 和 `connectionStrings` 值存储在 Azure 中，应用程序在 Azure 中运行时需要访问存储帐户和数据库。</span><span class="sxs-lookup"><span data-stu-id="fceb0-211">The environment creation script stores in Azure all of the `appSettings` and `connectionStrings` values that the application needs to access the storage account and databases when it runs in Azure.</span></span>

[!code-powershell[Main](automate-everything/samples/sample15.ps1)]

[!code-powershell[Main](automate-everything/samples/sample16.ps1)]

[!code-powershell[Main](automate-everything/samples/sample17.ps1?highlight=2)]

<span data-ttu-id="fceb0-212">[新 Relic](http://newrelic.com/)是一个遥测框架，在 "[监视和遥测](monitoring-and-telemetry.md)" 一章中演示。</span><span class="sxs-lookup"><span data-stu-id="fceb0-212">[New Relic](http://newrelic.com/) is a telemetry framework that we demonstrate in the [Monitoring and Telemetry](monitoring-and-telemetry.md) chapter.</span></span> <span data-ttu-id="fceb0-213">环境创建脚本还会重启 web 应用，以确保它选取新的 Relic 设置。</span><span class="sxs-lookup"><span data-stu-id="fceb0-213">The environment creation script also restarts the web app to make sure that it picks up the New Relic settings.</span></span>

[!code-powershell[Main](automate-everything/samples/sample18.ps1?highlight=2)]

### <a name="preparing-for-deployment"></a><span data-ttu-id="fceb0-214">准备部署</span><span class="sxs-lookup"><span data-stu-id="fceb0-214">Preparing for deployment</span></span>

<span data-ttu-id="fceb0-215">在该过程结束时，环境创建脚本将调用两个函数来创建部署脚本将使用的文件。</span><span class="sxs-lookup"><span data-stu-id="fceb0-215">At the end of the process, the environment creation script calls two functions to create files that will be used by the deployment script.</span></span>

<span data-ttu-id="fceb0-216">其中一个函数将创建发布配置文件 *（&lt;websitename&gt;.pubxml*文件）。</span><span class="sxs-lookup"><span data-stu-id="fceb0-216">One of these functions creates a publish profile *(&lt;websitename&gt;.pubxml* file).</span></span> <span data-ttu-id="fceb0-217">此代码调用 Azure REST API 以获取发布设置，并将信息保存在 *.publishsettings*文件中。</span><span class="sxs-lookup"><span data-stu-id="fceb0-217">The code calls the Azure REST API to get the publish settings, and it saves the information in a *.publishsettings* file.</span></span> <span data-ttu-id="fceb0-218">然后，它将使用该文件中的信息以及模板文件（ *.pubxml*）来创建包含发布配置文件的 *.pubxml*文件。</span><span class="sxs-lookup"><span data-stu-id="fceb0-218">Then it uses the information from that file along with a template file (*pubxml.template*) to create the *.pubxml* file that contains the publish profile.</span></span> <span data-ttu-id="fceb0-219">此两步过程模拟您在 Visual Studio 中执行的操作：下载 *.publishsettings*文件并导入以创建发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="fceb0-219">This two-step process simulates what you do in Visual Studio: download a *.publishsettings* file and import that to create a publish profile.</span></span>

<span data-ttu-id="fceb0-220">另一个函数使用另一个模板文件（网站环境模板）创建*website-environment*文件，其中包含部署脚本将与 *.pubxml*文件一起使用的设置。</span><span class="sxs-lookup"><span data-stu-id="fceb0-220">The other function uses another template file (website-environment.template) to create a *website-environment.xml* file that contains settings the deployment script will use along with the *.pubxml* file.</span></span>

### <a name="troubleshooting-and-error-handling"></a><span data-ttu-id="fceb0-221">疑难解答和错误处理</span><span class="sxs-lookup"><span data-stu-id="fceb0-221">Troubleshooting and error handling</span></span>

<span data-ttu-id="fceb0-222">脚本类似于程序：它们可能会失败，并且当用户需要了解失败和导致错误的原因时，它们也会失败。</span><span class="sxs-lookup"><span data-stu-id="fceb0-222">Scripts are like programs: they can fail, and when they do you want to know as much as you can about the failure and what caused it.</span></span> <span data-ttu-id="fceb0-223">出于此原因，环境创建脚本会将 `VerbosePreference` 变量的值从 `SilentlyContinue` 更改为 `Continue`，以便显示所有详细消息。</span><span class="sxs-lookup"><span data-stu-id="fceb0-223">For this reason, the environment creation script changes the value of the `VerbosePreference` variable from `SilentlyContinue` to `Continue` so that all verbose messages are displayed.</span></span> <span data-ttu-id="fceb0-224">它还会将 `ErrorActionPreference` 变量的值从 `Continue` 更改为 `Stop`，以便即使在遇到非终止错误时，脚本也会停止：</span><span class="sxs-lookup"><span data-stu-id="fceb0-224">It also changes the value of the `ErrorActionPreference` variable from `Continue` to `Stop`, so that the script stops even when it encounters non-terminating errors:</span></span>

[!code-powershell[Main](automate-everything/samples/sample19.ps1)]

<span data-ttu-id="fceb0-225">在执行任何工作之前，该脚本会存储开始时间，以便它可以计算完成所用的时间：</span><span class="sxs-lookup"><span data-stu-id="fceb0-225">Before it does any work, the script stores the start time so that it can calculate the elapsed time when it's done:</span></span>

[!code-powershell[Main](automate-everything/samples/sample20.ps1)]

<span data-ttu-id="fceb0-226">工作完成后，该脚本将显示运行时间：</span><span class="sxs-lookup"><span data-stu-id="fceb0-226">After it completes its work, the script displays the elapsed time:</span></span>

[!code-powershell[Main](automate-everything/samples/sample21.ps1)]

<span data-ttu-id="fceb0-227">对于每个键操作，该脚本将编写详细消息，例如：</span><span class="sxs-lookup"><span data-stu-id="fceb0-227">And for every key operation the script writes verbose messages, for example:</span></span>

[!code-powershell[Main](automate-everything/samples/sample22.ps1)]

## <a name="deployment-script"></a><span data-ttu-id="fceb0-228">部署脚本</span><span class="sxs-lookup"><span data-stu-id="fceb0-228">Deployment script</span></span>

<span data-ttu-id="fceb0-229">*New-AzureWebsiteEnv*脚本在创建环境时执行的操作， *Publish-AzureWebsite*脚本用于部署应用程序。</span><span class="sxs-lookup"><span data-stu-id="fceb0-229">What the *New-AzureWebsiteEnv.ps1* script does for environment creation, the *Publish-AzureWebsite.ps1* script does for application deployment.</span></span>

<span data-ttu-id="fceb0-230">部署脚本从环境创建脚本创建的*website-environment*文件中获取 web 应用的名称。</span><span class="sxs-lookup"><span data-stu-id="fceb0-230">The deployment script gets the name of the web app from the *website-environment.xml* file created by the environment creation script.</span></span>

[!code-powershell[Main](automate-everything/samples/sample23.ps1)]

<span data-ttu-id="fceb0-231">它从 *.publishsettings*文件中获取部署用户密码：</span><span class="sxs-lookup"><span data-stu-id="fceb0-231">It gets the deployment user password from the *.publishsettings* file:</span></span>

[!code-powershell[Main](automate-everything/samples/sample24.ps1)]

<span data-ttu-id="fceb0-232">它执行生成和部署项目的[MSBuild](http://msbuildbook.com/)命令：</span><span class="sxs-lookup"><span data-stu-id="fceb0-232">It executes the [MSBuild](http://msbuildbook.com/) command that builds and deploys the project:</span></span>

[!code-powershell[Main](automate-everything/samples/sample25.ps1)]

<span data-ttu-id="fceb0-233">如果已在命令行中指定 `Launch` 参数，它将调用 `Show-AzureWebsite` cmdlet，以将默认浏览器打开到网站 URL。</span><span class="sxs-lookup"><span data-stu-id="fceb0-233">And if you've specified the `Launch` parameter on the command line, it calls the `Show-AzureWebsite` cmdlet to open your default browser to the website URL.</span></span>

[!code-powershell[Main](automate-everything/samples/sample26.ps1?highlight=3)]

<span data-ttu-id="fceb0-234">可以使用如下命令运行部署脚本：</span><span class="sxs-lookup"><span data-stu-id="fceb0-234">You can run the deployment script with a command like this one:</span></span>

`.\Publish-AzureWebsite.ps1 ..\MyFixIt\MyFixIt.csproj -Launch`

<span data-ttu-id="fceb0-235">完成后，浏览器将打开，并在云中运行 `<websitename>.azurewebsites.net` URL 处运行的站点。</span><span class="sxs-lookup"><span data-stu-id="fceb0-235">And when it's done, the browser opens with the site running in the cloud at the `<websitename>.azurewebsites.net` URL.</span></span>

![修复部署到 Windows Azure 的 It 应用](automate-everything/_static/image7.png)

## <a name="summary"></a><span data-ttu-id="fceb0-237">总结</span><span class="sxs-lookup"><span data-stu-id="fceb0-237">Summary</span></span>

<span data-ttu-id="fceb0-238">使用这些脚本，可以确信相同的步骤将始终使用相同的顺序执行。</span><span class="sxs-lookup"><span data-stu-id="fceb0-238">With these scripts you can be confident that the same steps will always be executed in the same order using the same options.</span></span> <span data-ttu-id="fceb0-239">这有助于确保团队中的每个开发人员不会错过某些事情，或在自己的计算机上部署自定义的内容，或将其部署到其他团队成员环境或生产环境中。</span><span class="sxs-lookup"><span data-stu-id="fceb0-239">This helps ensure that each developer on the team doesn't miss something or mess something up or deploy something custom on his own machine that won't actually work the same way in another team member's environment or in production.</span></span>

<span data-ttu-id="fceb0-240">同样，可以通过使用可在 Linux 或 Mac 上运行的 REST API、Windows PowerShell 脚本、.NET 语言 API 或 Bash 实用程序，自动执行大多数可以在管理门户中执行的 Azure 管理功能。</span><span class="sxs-lookup"><span data-stu-id="fceb0-240">In a similar way, you can automate most Azure management functions that you can do in the management portal, by using the REST API, Windows PowerShell scripts, a .NET language API, or a Bash utility that you can run on Linux or Mac.</span></span>

<span data-ttu-id="fceb0-241">在[下一章](source-control.md)中，我们将介绍源代码，并解释在源代码存储库中包含脚本非常重要的原因。</span><span class="sxs-lookup"><span data-stu-id="fceb0-241">In the [next chapter](source-control.md) we'll look at source code and explain why it's important to include your scripts in your source code repository.</span></span>

## <a name="resources"></a><span data-ttu-id="fceb0-242">资源</span><span class="sxs-lookup"><span data-stu-id="fceb0-242">Resources</span></span>

- <span data-ttu-id="fceb0-243">[安装和配置适用于 Azure 的 Windows PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1)。</span><span class="sxs-lookup"><span data-stu-id="fceb0-243">[Install and Configure Windows PowerShell for Azure](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1).</span></span> <span data-ttu-id="fceb0-244">说明如何安装 Azure PowerShell cmdlet 以及如何在计算机上安装所需的证书，以便管理 Azure 帐户。</span><span class="sxs-lookup"><span data-stu-id="fceb0-244">Explains how to install the Azure PowerShell cmdlets and how to install the certificate that you need on your computer in order to manage your Azure account.</span></span> <span data-ttu-id="fceb0-245">这是一个很好的入门教程，因为它还包含指向用于学习 PowerShell 本身的资源的链接。</span><span class="sxs-lookup"><span data-stu-id="fceb0-245">This is a great place to get started because it also has links to resources for learning PowerShell itself.</span></span>
- <span data-ttu-id="fceb0-246">[Azure 脚本中心](https://docs.microsoft.com/azure/automation/automation-runbook-gallery)。</span><span class="sxs-lookup"><span data-stu-id="fceb0-246">[Azure Script Center](https://docs.microsoft.com/azure/automation/automation-runbook-gallery).</span></span> <span data-ttu-id="fceb0-247">用于开发管理 Azure 服务的脚本的资源的 WindowsAzure.com 门户，其中包含入门教程、cmdlet 参考文档和源代码以及示例脚本的链接</span><span class="sxs-lookup"><span data-stu-id="fceb0-247">WindowsAzure.com portal to resources for developing scripts that manage Azure services, with links to getting started tutorials, cmdlet reference documentation and source code, and sample scripts</span></span>
- <span data-ttu-id="fceb0-248">[周末脚本编写：通过 Azure 和 PowerShell 入门](https://blogs.technet.com/b/heyscriptingguy/archive/2013/06/22/weekend-scripter-getting-started-with-windows-azure-and-powershell.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fceb0-248">[Weekend Scripter: Getting Started with Azure and PowerShell](https://blogs.technet.com/b/heyscriptingguy/archive/2013/06/22/weekend-scripter-getting-started-with-windows-azure-and-powershell.aspx).</span></span> <span data-ttu-id="fceb0-249">在专用于 Windows PowerShell 的博客中，这篇文章提供了有关使用 PowerShell 进行 Azure 管理功能的很好的介绍。</span><span class="sxs-lookup"><span data-stu-id="fceb0-249">In a blog dedicated to Windows PowerShell, this post provides a great introduction to using PowerShell for Azure management functions.</span></span>
- <span data-ttu-id="fceb0-250">[安装和配置 Azure 跨平台命令行界面](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest)。</span><span class="sxs-lookup"><span data-stu-id="fceb0-250">[Install and Configure the Azure Cross-Platform Command-Line Interface](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest).</span></span> <span data-ttu-id="fceb0-251">适用于 Azure 脚本编写框架的入门教程，适用于 Mac 和 Linux 以及 Windows 系统。</span><span class="sxs-lookup"><span data-stu-id="fceb0-251">Getting-started tutorial for an Azure scripting framework that works on Mac and Linux as well as Windows systems.</span></span>
- <span data-ttu-id="fceb0-252">[下载 Azure sdk 和工具主题的命令行工具](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="fceb0-252">[Command-line tools section of the Download Azure SDKs and Tools topic](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="fceb0-253">与适用于 Azure 的命令行工具相关的文档和下载的门户页。</span><span class="sxs-lookup"><span data-stu-id="fceb0-253">Portal page for documentation and downloads related to command-line tools for Azure.</span></span>
- <span data-ttu-id="fceb0-254">[通过 Azure 管理库和 .net 使一切自动化](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fceb0-254">[Automating everything with the Azure Management Libraries and .NET](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx).</span></span> <span data-ttu-id="fceb0-255">Scott Hanselman 介绍了适用于 Azure 的 .NET 管理 API。</span><span class="sxs-lookup"><span data-stu-id="fceb0-255">Scott Hanselman introduces the .NET management API for Azure.</span></span>
- <span data-ttu-id="fceb0-256">[使用 Windows PowerShell 脚本发布到开发和测试环境](https://msdn.microsoft.com/library/azure/dn642480.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fceb0-256">[Using Windows PowerShell Scripts to Publish to Dev and Test Environments](https://msdn.microsoft.com/library/azure/dn642480.aspx).</span></span> <span data-ttu-id="fceb0-257">介绍如何使用 Visual Studio 为 web 项目自动生成的发布脚本的 MSDN 文档。</span><span class="sxs-lookup"><span data-stu-id="fceb0-257">MSDN documentation that explains how to use publish scripts that Visual Studio automatically generates for web projects.</span></span>
- <span data-ttu-id="fceb0-258">[PowerShell Tools for Visual Studio 2013](https://visualstudiogallery.msdn.microsoft.com/c9eb3ba8-0c59-4944-9a62-6eee37294597)。</span><span class="sxs-lookup"><span data-stu-id="fceb0-258">[PowerShell Tools for Visual Studio 2013](https://visualstudiogallery.msdn.microsoft.com/c9eb3ba8-0c59-4944-9a62-6eee37294597).</span></span> <span data-ttu-id="fceb0-259">Visual Studio 扩展，在 Visual Studio 中为 Windows PowerShell 添加语言支持。</span><span class="sxs-lookup"><span data-stu-id="fceb0-259">Visual Studio extension that adds language support for Windows PowerShell in Visual Studio.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="fceb0-260">[上一页](introduction.md)
> [下一页](source-control.md)</span><span class="sxs-lookup"><span data-stu-id="fceb0-260">[Previous](introduction.md)
[Next](source-control.md)</span></span>
