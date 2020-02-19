---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control
title: 源代码管理（通过 Azure 构建实际的云应用） |Microsoft Docs
author: MikeWasson
description: 使用 Azure 电子书构建真实的云应用基于 Scott Guthrie 开发的演示文稿。 它介绍了13种模式和实践，
ms.author: riande
ms.date: 06/23/2015
ms.assetid: 2a0370d3-c2fb-4bf3-88b8-aad5a736c793
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control
msc.type: authoredcontent
ms.openlocfilehash: 5a1e0d7cd3c396d4be79c8958422602055eb3db1
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457097"
---
# <a name="source-control-building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="83d32-104">源代码管理（通过 Azure 构建实际的云应用）</span><span class="sxs-lookup"><span data-stu-id="83d32-104">Source Control (Building Real-World Cloud Apps with Azure)</span></span>

<span data-ttu-id="83d32-105">作者： [Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://twitter.com/RickAndMSFT)， [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="83d32-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="83d32-106">[下载 Fix It 项目](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="83d32-106">[Download Fix It Project](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) or [Download E-book](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span></span>

> <span data-ttu-id="83d32-107">**使用 Azure 电子书构建真实的云应用**基于 Scott Guthrie 开发的演示文稿。</span><span class="sxs-lookup"><span data-stu-id="83d32-107">The **Building Real World Cloud Apps with Azure** e-book is based on a presentation developed by Scott Guthrie.</span></span> <span data-ttu-id="83d32-108">它介绍了可帮助你成功开发云的 web 应用的13种模式和实践。</span><span class="sxs-lookup"><span data-stu-id="83d32-108">It explains 13 patterns and practices that can help you be successful developing web apps for the cloud.</span></span> <span data-ttu-id="83d32-109">有关电子书的信息，请参阅[第一章](introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="83d32-109">For information about the e-book, see [the first chapter](introduction.md).</span></span>

<span data-ttu-id="83d32-110">源代码管理对于所有云开发项目（而不仅仅是团队环境）都是必不可少的。</span><span class="sxs-lookup"><span data-stu-id="83d32-110">Source control is essential for all cloud development projects, not just team environments.</span></span> <span data-ttu-id="83d32-111">您不想编辑源代码，甚至无需使用 undo 函数和自动备份的 Word 文档，而且源代码管理可在项目级提供这些函数，在这种情况下，在出现错误时，它们可以节省更多的时间。</span><span class="sxs-lookup"><span data-stu-id="83d32-111">You wouldn't think of editing source code or even a Word document without an undo function and automatic backups, and source control gives you those functions at a project level where they can save even more time when something goes wrong.</span></span> <span data-ttu-id="83d32-112">使用云源代码管理服务，你无需担心复杂的设置，你可以免费使用最多5个用户的 Azure Repos 源代码管理。</span><span class="sxs-lookup"><span data-stu-id="83d32-112">With cloud source control services, you no longer have to worry about complicated set-up, and you can use Azure Repos source control free for up to 5 users.</span></span>

<span data-ttu-id="83d32-113">本章的第一部分介绍了需要注意的三个关键最佳方案：</span><span class="sxs-lookup"><span data-stu-id="83d32-113">The first part of this chapter explains three key best practices to keep in mind:</span></span>

- <span data-ttu-id="83d32-114">将[自动化脚本视为源代码](#scripts)，并将其与应用程序代码结合在一起。</span><span class="sxs-lookup"><span data-stu-id="83d32-114">[Treat automation scripts as source code](#scripts) and version them together with your application code.</span></span>
- <span data-ttu-id="83d32-115">[切勿将机密](#secrets)（敏感数据，如凭据）签入到源代码存储库中。</span><span class="sxs-lookup"><span data-stu-id="83d32-115">[Never check in secrets](#secrets) (sensitive data such as credentials) into a source code repository.</span></span>
- <span data-ttu-id="83d32-116">[设置源分支](#devops)以启用 DevOps 工作流。</span><span class="sxs-lookup"><span data-stu-id="83d32-116">[Set up source branches](#devops) to enable the DevOps workflow.</span></span>

<span data-ttu-id="83d32-117">本章的其余部分提供 Visual Studio、Azure 和 Azure Repos 中这些模式的一些示例实现：</span><span class="sxs-lookup"><span data-stu-id="83d32-117">The remainder of the chapter gives some sample implementations of these patterns in Visual Studio, Azure, and Azure Repos:</span></span>

- [<span data-ttu-id="83d32-118">向 Visual Studio 中的源代码管理添加脚本</span><span class="sxs-lookup"><span data-stu-id="83d32-118">Add scripts to source control in Visual Studio</span></span>](#vsscripts)
- [<span data-ttu-id="83d32-119">在 Azure 中存储敏感数据</span><span class="sxs-lookup"><span data-stu-id="83d32-119">Store sensitive data in Azure</span></span>](#appsettings)
- [<span data-ttu-id="83d32-120">在 Visual Studio 中使用 Git 并 Azure Repos</span><span class="sxs-lookup"><span data-stu-id="83d32-120">Use Git in Visual Studio and Azure Repos</span></span>](#gittfs)

<a id="scripts"></a>
## <a name="treat-automation-scripts-as-source-code"></a><span data-ttu-id="83d32-121">将自动化脚本视为源代码</span><span class="sxs-lookup"><span data-stu-id="83d32-121">Treat automation scripts as source code</span></span>

<span data-ttu-id="83d32-122">当你在云项目上工作时，你会经常更改操作，并且你希望能够快速应对你的客户报告的问题。</span><span class="sxs-lookup"><span data-stu-id="83d32-122">When you're working on a cloud project you're changing things frequently and you want to be able to react quickly to issues reported by your customers.</span></span> <span data-ttu-id="83d32-123">响应速度很快涉及使用自动化脚本，如 "[自动化一切](automate-everything.md)" 一章中所述。</span><span class="sxs-lookup"><span data-stu-id="83d32-123">Responding quickly involves using automation scripts, as explained in the [Automate Everything](automate-everything.md) chapter.</span></span> <span data-ttu-id="83d32-124">需要与应用程序源代码同步，用于创建你的环境、部署到该环境、进行缩放、扩展等的所有脚本。</span><span class="sxs-lookup"><span data-stu-id="83d32-124">All of the scripts that you use to create your environment, deploy to it, scale it, etc., need to be in sync with your application source code.</span></span>

<span data-ttu-id="83d32-125">若要使脚本与代码保持同步，请将脚本存储在源代码管理系统中。</span><span class="sxs-lookup"><span data-stu-id="83d32-125">To keep scripts in sync with code, store them in your source control system.</span></span> <span data-ttu-id="83d32-126">然后，如果您需要回滚更改或快速修复与开发代码不同的生产代码，则无需浪费时间来尝试跟踪已更改的设置或哪些团队成员拥有所需版本的副本。</span><span class="sxs-lookup"><span data-stu-id="83d32-126">Then if you ever need to roll back changes or make a quick fix to production code which is different from development code, you don't have to waste time trying to track down which settings have changed or which team members have copies of the version you need.</span></span> <span data-ttu-id="83d32-127">您可以确信，所需的脚本与需要它们的基本代码同步，并确保所有团队成员都能使用相同的脚本。</span><span class="sxs-lookup"><span data-stu-id="83d32-127">You're assured that the scripts you need are in sync with the code base that you need them for, and you're assured that all team members are working with the same scripts.</span></span> <span data-ttu-id="83d32-128">然后，无论是否需要将热修补程序自动部署和部署到生产环境或新功能开发中，都可以使用正确的脚本来编写需要更新的代码。</span><span class="sxs-lookup"><span data-stu-id="83d32-128">Then whether you need to automate testing and deployment of a hot fix to production or new feature development, you'll have the right script for the code that needs to be updated.</span></span>

<a id="secrets"></a>
## <a name="dont-check-in-secrets"></a><span data-ttu-id="83d32-129">不签入机密</span><span class="sxs-lookup"><span data-stu-id="83d32-129">Don't check in secrets</span></span>

<span data-ttu-id="83d32-130">通常很多人都可以访问源代码存储库，因为它是敏感数据（如密码）的适当安全位置。</span><span class="sxs-lookup"><span data-stu-id="83d32-130">A source code repository is typically accessible to too many people for it to be an appropriately secure place for sensitive data such as passwords.</span></span> <span data-ttu-id="83d32-131">如果脚本依赖于机密（如密码），请将这些设置参数化，使其不会保存在源代码中，并将机密存储在其他位置。</span><span class="sxs-lookup"><span data-stu-id="83d32-131">If scripts rely on secrets such as passwords, parameterize those settings so that they don't get saved in source code, and store your secrets somewhere else.</span></span>

<span data-ttu-id="83d32-132">例如，Azure 允许你下载包含发布设置的文件，以便自动创建发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="83d32-132">For example, Azure lets you download files that contain publish settings in order to automate the creation of publish profiles.</span></span> <span data-ttu-id="83d32-133">这些文件包括有权管理 Azure 服务的用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="83d32-133">These files include user names and passwords that are authorized to manage your Azure services.</span></span> <span data-ttu-id="83d32-134">如果你使用此方法创建发布配置文件，并且将这些文件签入到源代码管理，则可以访问存储库的任何人都可以看到这些用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="83d32-134">If you use this method to create publish profiles, and if you check in these files to source control, anyone with access to your repository can see those user names and passwords.</span></span> <span data-ttu-id="83d32-135">您可以安全地将密码存储在发布配置文件中，因为它已加密，并且位于默认情况下不包含在源控件中的 *.pubxml*文件中。</span><span class="sxs-lookup"><span data-stu-id="83d32-135">You can safely store the password in the publish profile itself because it's encrypted and it's in a *.pubxml.user* file that by default is not included in source control.</span></span>

<a id="devops"></a>
## <a name="structure-source-branches-to-facilitate-devops-workflow"></a><span data-ttu-id="83d32-136">用于促进 DevOps 工作流的结构源分支</span><span class="sxs-lookup"><span data-stu-id="83d32-136">Structure source branches to facilitate DevOps workflow</span></span>

<span data-ttu-id="83d32-137">你在存储库中实现分支的方式会影响你开发新功能和解决生产中的问题的能力。</span><span class="sxs-lookup"><span data-stu-id="83d32-137">How you implement branches in your repository affects your ability to both develop new features and fix issues in production.</span></span> <span data-ttu-id="83d32-138">下面是大量中型团队使用的一种模式：</span><span class="sxs-lookup"><span data-stu-id="83d32-138">Here is a pattern that a lot of medium sized teams use:</span></span>

![源分支结构](source-control/_static/image1.png)

<span data-ttu-id="83d32-140">主分支始终与生产中的代码匹配。</span><span class="sxs-lookup"><span data-stu-id="83d32-140">The master branch always matches code that is in production.</span></span> <span data-ttu-id="83d32-141">Master 下的分支对应开发生命周期中的不同阶段。</span><span class="sxs-lookup"><span data-stu-id="83d32-141">Branches underneath master correspond to different stages in the development life cycle.</span></span> <span data-ttu-id="83d32-142">开发分支是实现新功能的地方。</span><span class="sxs-lookup"><span data-stu-id="83d32-142">The development branch is where you implement new features.</span></span> <span data-ttu-id="83d32-143">对于小团队而言，你可能只是具有母版和开发，但我们通常建议用户在开发和主服务器之间具有过渡分支。</span><span class="sxs-lookup"><span data-stu-id="83d32-143">For a small team you might just have master and development, but we often recommend that people have a staging branch between development and master.</span></span> <span data-ttu-id="83d32-144">在将更新转移到生产环境之前，可以使用过渡进行最终集成测试。</span><span class="sxs-lookup"><span data-stu-id="83d32-144">You can use staging for final integration testing before an update is moved to production.</span></span>

<span data-ttu-id="83d32-145">对于大型团队，每个新功能可能有单独的分支;对于较小的团队，你可能会让每个人都签入开发分支。</span><span class="sxs-lookup"><span data-stu-id="83d32-145">For big teams there may be separate branches for each new feature; for a smaller team you might have everyone checking in to the development branch.</span></span>

<span data-ttu-id="83d32-146">如果每个功能都有一个分支，则当功能 A 准备就绪时，将其源代码更改向上合并到开发分支，并向下合并到其他功能分支。</span><span class="sxs-lookup"><span data-stu-id="83d32-146">If you have a branch for each feature, when Feature A is ready you merge its source code changes up into the development branch and down into the other feature branches.</span></span> <span data-ttu-id="83d32-147">此源代码合并过程可能非常耗时，若要避免这种工作，同时保持单独的功能，某些团队还实现了一种称为 " *[功能切换](http://en.wikipedia.org/wiki/Feature_toggle)* " 的替代方法（也称为*功能标志*）。</span><span class="sxs-lookup"><span data-stu-id="83d32-147">This source code merging process can be time-consuming, and to avoid that work while still keeping features separate, some teams implement an alternative called *[feature toggles](http://en.wikipedia.org/wiki/Feature_toggle)* (also known as *feature flags*).</span></span> <span data-ttu-id="83d32-148">这意味着所有功能的所有代码都在相同的分支中，但你可以通过使用代码中的开关来启用或禁用每个功能。</span><span class="sxs-lookup"><span data-stu-id="83d32-148">This means all of the code for all of the features is in the same branch, but you enable or disable each feature by using switches in the code.</span></span> <span data-ttu-id="83d32-149">例如，假设功能 A 是用于修复 It 应用任务的新字段，功能 B 添加了缓存功能。</span><span class="sxs-lookup"><span data-stu-id="83d32-149">For example, suppose Feature A is a new field for Fix It app tasks, and Feature B adds caching functionality.</span></span> <span data-ttu-id="83d32-150">这两种功能的代码可以在开发分支中进行，但在将变量设置为 true 时，应用程序将只显示新字段，并且在其他变量设置为 true 时，它将仅使用缓存。</span><span class="sxs-lookup"><span data-stu-id="83d32-150">The code for both features can be in the development branch, but the app will only display the new field when a variable is set to true, and it will only use caching when a different variable is set to true.</span></span> <span data-ttu-id="83d32-151">如果功能 A 未准备好进行升级，但功能 B 已准备就绪，则可以将所有代码升级到生产，并将功能切换为 "关闭"，并打开功能 B 开关。</span><span class="sxs-lookup"><span data-stu-id="83d32-151">If Feature A isn't ready to be promoted but the Feature B is ready, you can promote all of the code to Production with the Feature A switch off and the Feature B switch on.</span></span> <span data-ttu-id="83d32-152">然后，你可以完成功能 A 并稍后升级，所有这些操作都不会合并源代码。</span><span class="sxs-lookup"><span data-stu-id="83d32-152">You can then finish Feature A and promote it later, all with no source code merging.</span></span>

<span data-ttu-id="83d32-153">无论你是使用分支还是切换功能，这种类似的分支结构都使你能够以敏捷且可重复的方式将你的代码从开发环境传输到生产中。</span><span class="sxs-lookup"><span data-stu-id="83d32-153">Whether or not you use branches or toggles for features, a branching structure like this enables you to flow your code from development into production in an agile and repeatable way.</span></span>

<span data-ttu-id="83d32-154">利用此结构，你还可以快速响应客户反馈。</span><span class="sxs-lookup"><span data-stu-id="83d32-154">This structure also enables you to react quickly to customer feedback.</span></span> <span data-ttu-id="83d32-155">如果需要快速修复生产，还可以采用敏捷的方式高效地执行此操作。</span><span class="sxs-lookup"><span data-stu-id="83d32-155">If you need to make a quick fix to production, you can also do that efficiently in an agile way.</span></span> <span data-ttu-id="83d32-156">你可以从主节点或过渡版创建分支，并在准备好将其合并到主分支和功能分支中。</span><span class="sxs-lookup"><span data-stu-id="83d32-156">You can create a branch off of master or staging, and when it's ready merge it up into master and down into development and feature branches.</span></span>

![修补程序分支](source-control/_static/image2.png)

<span data-ttu-id="83d32-158">如果没有类似于此的分支结构与生产和开发分支分离，则生产问题可能会让你进入升级新功能代码和生产修补程序的位置。</span><span class="sxs-lookup"><span data-stu-id="83d32-158">Without a branching structure like this with its separation of production and development branches, a production problem could put you in the position of having to promote new feature code along with your production fix.</span></span> <span data-ttu-id="83d32-159">新功能代码可能未经过充分测试并可投入生产，你可能需要执行大量工作来备份尚未准备好的更改。</span><span class="sxs-lookup"><span data-stu-id="83d32-159">The new feature code might not be fully tested and ready for production and you might have to do a lot of work backing out changes that aren't ready.</span></span> <span data-ttu-id="83d32-160">或者你可能需要延迟你的修复，才能测试更改并使其做好部署准备。</span><span class="sxs-lookup"><span data-stu-id="83d32-160">Or you might have to delay your fix in order to test changes and get them ready to deploy.</span></span>

<span data-ttu-id="83d32-161">接下来，你将看到有关如何在 Visual Studio、Azure 和 Azure Repos 中实现这三种模式的示例。</span><span class="sxs-lookup"><span data-stu-id="83d32-161">Next you'll see examples of how to implement these three patterns in Visual Studio, Azure, and Azure Repos.</span></span> <span data-ttu-id="83d32-162">这些是示例，而不是详细的分步操作说明;有关提供所有必要上下文的详细说明，请参阅本章末尾的[资源](#resources)部分。</span><span class="sxs-lookup"><span data-stu-id="83d32-162">These are examples rather than detailed step-by-step how-to-do-it instructions; for detailed instructions that provide all of the context necessary, see the [Resources](#resources) section at the end of the chapter.</span></span>

<a id="vsscripts"></a>
## <a name="add-scripts-to-source-control-in-visual-studio"></a><span data-ttu-id="83d32-163">向 Visual Studio 中的源代码管理添加脚本</span><span class="sxs-lookup"><span data-stu-id="83d32-163">Add scripts to source control in Visual Studio</span></span>

<span data-ttu-id="83d32-164">可以通过将脚本包含在 Visual Studio 解决方案文件夹（假定项目在源代码管理中），将其添加到 Visual Studio 中的源代码管理。</span><span class="sxs-lookup"><span data-stu-id="83d32-164">You can add scripts to source control in Visual Studio by including them in a Visual Studio solution folder (assuming your project is in source control).</span></span> <span data-ttu-id="83d32-165">下面是执行此操作的一种方法。</span><span class="sxs-lookup"><span data-stu-id="83d32-165">Here's one way to do it.</span></span>

<span data-ttu-id="83d32-166">在解决方案文件夹中为脚本创建一个文件夹（与 *.sln*文件相同的文件夹）。</span><span class="sxs-lookup"><span data-stu-id="83d32-166">Create a folder for the scripts in your solution folder (the same folder that has your *.sln* file).</span></span>

![自动化文件夹](source-control/_static/image3.png)

<span data-ttu-id="83d32-168">将脚本文件复制到该文件夹中。</span><span class="sxs-lookup"><span data-stu-id="83d32-168">Copy the script files into the folder.</span></span>

![自动化文件夹内容](source-control/_static/image4.png)

<span data-ttu-id="83d32-170">在 Visual Studio 中，将解决方案文件夹添加到项目。</span><span class="sxs-lookup"><span data-stu-id="83d32-170">In Visual Studio, add a solution folder to the project.</span></span>

![新解决方案文件夹菜单选择](source-control/_static/image5.png)

<span data-ttu-id="83d32-172">并将脚本文件添加到解决方案文件夹中。</span><span class="sxs-lookup"><span data-stu-id="83d32-172">And add the script files to the solution folder.</span></span>

!["添加现有项" 菜单选择](source-control/_static/image6.png)

![“添加现有项”对话框](source-control/_static/image7.png)

<span data-ttu-id="83d32-175">脚本文件现在已包含在项目中，源代码管理正在跟踪其版本更改以及相应的源代码更改。</span><span class="sxs-lookup"><span data-stu-id="83d32-175">The script files are now included in your project and source control is tracking their version changes along with corresponding source code changes.</span></span>

<a id="appsettings"></a>
## <a name="store-sensitive-data-in-azure"></a><span data-ttu-id="83d32-176">在 Azure 中存储敏感数据</span><span class="sxs-lookup"><span data-stu-id="83d32-176">Store sensitive data in Azure</span></span>

<span data-ttu-id="83d32-177">如果在 Azure 网站中运行应用程序，避免在源代码管理中存储凭据的一种方法是将其存储在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="83d32-177">If you run your application in an Azure Web Site, one way to avoid storing credentials in source control is to store them in Azure instead.</span></span>

<span data-ttu-id="83d32-178">例如，Fix It 应用程序在其 Web.config 文件中存储两个将在生产中使用密码的连接字符串和一个提供对 Azure 存储帐户的访问权限的密钥。</span><span class="sxs-lookup"><span data-stu-id="83d32-178">For example, the Fix It application stores in its Web.config file two connection strings that will have passwords in production and a key that gives access to your Azure storage account.</span></span>

[!code-xml[Main](source-control/samples/sample1.xml?highlight=2-3,11)]

<span data-ttu-id="83d32-179">如果将这些设置的实际生产值放在 web.config*文件中*，或将它们放在 web.config 文件中来*配置 web.config 转换*以便在部署过程中插入它们，它们将存储在源存储库中。</span><span class="sxs-lookup"><span data-stu-id="83d32-179">If you put actual production values for these settings in your *Web.config* file, or if you put them in the *Web.Release.config* file to configure a Web.config transform to insert them during deployment, they'll be stored in the source repository.</span></span> <span data-ttu-id="83d32-180">如果将数据库连接字符串输入到生产发布配置文件中，则密码将位于 *.pubxml*文件中。</span><span class="sxs-lookup"><span data-stu-id="83d32-180">If you enter the database connection strings into the production publish profile, the password will be in your *.pubxml* file.</span></span> <span data-ttu-id="83d32-181">（您可以从源代码管理中排除 *.pubxml*文件，但这样就失去了共享所有其他部署设置所带来的好处。）</span><span class="sxs-lookup"><span data-stu-id="83d32-181">(You could exclude the *.pubxml* file from source control, but then you lose the benefit of sharing all the other deployment settings.)</span></span>

<span data-ttu-id="83d32-182">Azure 为你提供了*web.config*文件的 " **appSettings** " 和 "连接字符串" 部分的替代方法。</span><span class="sxs-lookup"><span data-stu-id="83d32-182">Azure gives you an alternative for the **appSettings** and connection strings sections of the *Web.config* file.</span></span> <span data-ttu-id="83d32-183">下面是 Azure 管理门户中网站的 "**配置**" 选项卡的相关部分：</span><span class="sxs-lookup"><span data-stu-id="83d32-183">Here is the relevant part of the **Configuration** tab for a web site in the Azure management portal:</span></span>

![门户中的 appSettings 和 connectionStrings](source-control/_static/image8.png)

<span data-ttu-id="83d32-185">将项目部署到此网站并运行应用程序时，在 Azure 中存储的任何值都会覆盖 Web.config 文件中的任何值。</span><span class="sxs-lookup"><span data-stu-id="83d32-185">When you deploy a project to this web site and the application runs, whatever values you have stored in Azure override whatever values are in the Web.config file.</span></span>

<span data-ttu-id="83d32-186">可以使用管理门户或脚本在 Azure 中设置这些值。</span><span class="sxs-lookup"><span data-stu-id="83d32-186">You can set these values in Azure by using either the management portal or scripts.</span></span> <span data-ttu-id="83d32-187">"[自动完成所有](automate-everything.md)操作" 一章中所述的环境创建自动化脚本将创建一个 Azure SQL 数据库，获取存储和 SQL 数据库连接字符串，并将这些机密存储在网站的设置中。</span><span class="sxs-lookup"><span data-stu-id="83d32-187">The environment creation automation script you saw in the [Automate Everything](automate-everything.md) chapter creates an Azure SQL Database, gets the storage and SQL Database connection strings, and stores these secrets in the settings for your web site.</span></span>

[!code-powershell[Main](source-control/samples/sample2.ps1)]

[!code-powershell[Main](source-control/samples/sample3.ps1)]

<span data-ttu-id="83d32-188">请注意，将对脚本进行参数化，以便不会将实际值保留到源存储库。</span><span class="sxs-lookup"><span data-stu-id="83d32-188">Notice that the scripts are parameterized so that actual values don't get persisted to the source repository.</span></span>

<span data-ttu-id="83d32-189">当你在开发环境中本地运行时，应用程序将读取本地 Web.config 文件，并且你的连接字符串指向 Web 项目的*应用\_数据*文件夹中的 LocalDB SQL Server 数据库。</span><span class="sxs-lookup"><span data-stu-id="83d32-189">When you run locally in your development environment, the app reads your local Web.config file and your connection string points to a LocalDB SQL Server database in the *App\_Data* folder of your web project.</span></span> <span data-ttu-id="83d32-190">当你在 Azure 中运行应用程序时，如果应用程序尝试从 web.config 文件中读取这些值，则它返回并使用的值是为网站存储的值，而不是在 Web.config 文件中的实际值。</span><span class="sxs-lookup"><span data-stu-id="83d32-190">When you run the app in Azure and the app tries to read these values from the Web.config file, what it gets back and uses are the values stored for the Web Site, not what's actually in Web.config file.</span></span>

<a id="gittfs"></a>
## <a name="use-git-in-visual-studio-and-azure-devops"></a><span data-ttu-id="83d32-191">在 Visual Studio 和 Azure DevOps 中使用 Git</span><span class="sxs-lookup"><span data-stu-id="83d32-191">Use Git in Visual Studio and Azure DevOps</span></span>

<span data-ttu-id="83d32-192">您可以使用任何源代码管理环境来实现前面介绍的 DevOps 分支结构。</span><span class="sxs-lookup"><span data-stu-id="83d32-192">You can use any source control environment to implement the DevOps branching structure presented earlier.</span></span> <span data-ttu-id="83d32-193">对于分布式团队而言，[分布式版本控制系统](http://en.wikipedia.org/wiki/Distributed_revision_control)（DVCS）可能效果最好;对于其他团队而言，[集中式系统](http://en.wikipedia.org/wiki/Revision_control)的工作效果可能更好。</span><span class="sxs-lookup"><span data-stu-id="83d32-193">For distributed teams a [distributed version control system](http://en.wikipedia.org/wiki/Distributed_revision_control) (DVCS) might work best; for other teams a [centralized system](http://en.wikipedia.org/wiki/Revision_control) might work better.</span></span>

<span data-ttu-id="83d32-194">[Git](http://git-scm.com/)是一种流行的分布式版本控制系统。</span><span class="sxs-lookup"><span data-stu-id="83d32-194">[Git](http://git-scm.com/) is a popular distributed version control system.</span></span> <span data-ttu-id="83d32-195">如果使用 Git 进行源代码管理，则会在本地计算机上创建该存储库的完整副本及其所有历史记录。</span><span class="sxs-lookup"><span data-stu-id="83d32-195">When you use Git for source control, you have a complete copy of the repository with all of its history on your local computer.</span></span> <span data-ttu-id="83d32-196">许多人更喜欢这样做，因为当你未连接到网络时，可以更轻松地继续工作-你可以继续执行提交和回滚、创建和切换分支等操作。</span><span class="sxs-lookup"><span data-stu-id="83d32-196">Many people prefer that because it's easier to continue working when you're not connected to the network -- you can continue to do commits and rollbacks, create and switch branches, and so forth.</span></span> <span data-ttu-id="83d32-197">即使你连接到网络，在所有内容都是本地的时，创建分支和切换分支会更简单快捷。</span><span class="sxs-lookup"><span data-stu-id="83d32-197">Even when you're connected to the network, it's easier and quicker to create branches and switch branches when everything is local.</span></span> <span data-ttu-id="83d32-198">你还可以执行本地提交和回滚，而不会影响其他开发人员。</span><span class="sxs-lookup"><span data-stu-id="83d32-198">You can also do local commits and rollbacks without having an impact on other developers.</span></span> <span data-ttu-id="83d32-199">并且，你可以在将提交发送到服务器之前批处理提交。</span><span class="sxs-lookup"><span data-stu-id="83d32-199">And you can batch commits before sending them to the server.</span></span>

<span data-ttu-id="83d32-200">[Azure Repos](/azure/devops/repos/index?view=vsts)提供[Git](/azure/devops/repos/git/?view=vsts)和[Team Foundation 版本控制](/azure/devops/repos/tfvc/index?view=vsts)（TFVC; 集中源代码管理）。</span><span class="sxs-lookup"><span data-stu-id="83d32-200">[Azure Repos](/azure/devops/repos/index?view=vsts) offers both [Git](/azure/devops/repos/git/?view=vsts) and [Team Foundation Version Control](/azure/devops/repos/tfvc/index?view=vsts) (TFVC; centralized source control).</span></span> <span data-ttu-id="83d32-201">[此处](https://app.vsaex.visualstudio.com/signup)提供 Azure DevOps 入门。</span><span class="sxs-lookup"><span data-stu-id="83d32-201">Get started with Azure DevOps [here](https://app.vsaex.visualstudio.com/signup).</span></span>

<span data-ttu-id="83d32-202">Visual Studio 2017 包含内置的一流[Git 支持](https://msdn.microsoft.com/library/hh850437.aspx)。</span><span class="sxs-lookup"><span data-stu-id="83d32-202">Visual Studio 2017 includes built-in, first-class [Git support](https://msdn.microsoft.com/library/hh850437.aspx).</span></span> <span data-ttu-id="83d32-203">下面是其工作原理的简要演示。</span><span class="sxs-lookup"><span data-stu-id="83d32-203">Here's a quick demo of how that works.</span></span>

<span data-ttu-id="83d32-204">在 Visual Studio 中打开项目后，在**解决方案资源管理器**中右键单击该解决方案，然后选择 "**将解决方案添加到源代码管理**"。</span><span class="sxs-lookup"><span data-stu-id="83d32-204">With a project open in Visual Studio, right-click the solution in **Solution Explorer**, and then choose **Add Solution to Source Control**.</span></span>

![将解决方案添加到源代码管理](source-control/_static/image9.png)

<span data-ttu-id="83d32-206">Visual Studio 会询问你是否要使用 TFVC （集中式版本控制）或 Git。</span><span class="sxs-lookup"><span data-stu-id="83d32-206">Visual Studio asks if you want to use TFVC (centralized version control) or Git.</span></span>

![选择源代码管理](source-control/_static/image10.png)

<span data-ttu-id="83d32-208">选择 Git 并单击 **"确定"** 时，Visual Studio 将在解决方案文件夹中创建一个新的本地 Git 存储库。</span><span class="sxs-lookup"><span data-stu-id="83d32-208">When you select Git and click **OK**, Visual Studio creates a new local Git repository in your solution folder.</span></span> <span data-ttu-id="83d32-209">新存储库尚无文件;必须通过执行 Git commit 将它们添加到存储库。</span><span class="sxs-lookup"><span data-stu-id="83d32-209">The new repository has no files yet; you have to add them to the repository by doing a Git commit.</span></span> <span data-ttu-id="83d32-210">在**解决方案资源管理器**中右键单击该解决方案，然后单击 "**提交**"。</span><span class="sxs-lookup"><span data-stu-id="83d32-210">Right-click the solution in **Solution Explorer**, and then click **Commit**.</span></span>

![Commit](source-control/_static/image11.png)

<span data-ttu-id="83d32-212">Visual Studio 会自动暂存提交的所有项目文件，并在 "**包含的更改**" 窗格中**团队资源管理器**列出它们。</span><span class="sxs-lookup"><span data-stu-id="83d32-212">Visual Studio automatically stages all of the project files for the commit and lists them in **Team Explorer** in the **Included Changes** pane.</span></span> <span data-ttu-id="83d32-213">（如果不想在提交中包含某些资源，请选择它们，右键单击，然后单击 "**排除**"。）</span><span class="sxs-lookup"><span data-stu-id="83d32-213">(If there were some you didn't want to include in the commit, you could select them, right-click, and click **Exclude**.)</span></span>

![Team Explorer](source-control/_static/image12.png)

<span data-ttu-id="83d32-215">输入提交注释，然后单击 "**提交**"，Visual Studio 将执行提交，并显示提交 ID。</span><span class="sxs-lookup"><span data-stu-id="83d32-215">Enter a commit comment and click **Commit**, and Visual Studio executes the commit and displays the commit ID.</span></span>

![团队资源管理器更改](source-control/_static/image13.png)

<span data-ttu-id="83d32-217">现在，如果您更改了某些代码，使其不同于存储库中的内容，则可以轻松查看不同之处。</span><span class="sxs-lookup"><span data-stu-id="83d32-217">Now if you change some code so that it's different from what's in the repository, you can easily view the differences.</span></span> <span data-ttu-id="83d32-218">右键单击已更改的文件，选择 "与未**修改的比较**"，将显示一个显示未提交更改的比较显示。</span><span class="sxs-lookup"><span data-stu-id="83d32-218">Right-click a file that you've changed, select **Compare with Unmodified**, and you get a comparison display that shows your uncommitted change.</span></span>

![与未修改的比较](source-control/_static/image14.png)

![显示更改的差异](source-control/_static/image15.png)

<span data-ttu-id="83d32-221">你可以轻松地查看正在进行的更改并将其签入。</span><span class="sxs-lookup"><span data-stu-id="83d32-221">You can easily see what changes you're making and check them in.</span></span>

<span data-ttu-id="83d32-222">假设您需要创建一个分支，也可以在 Visual Studio 中执行此操作。</span><span class="sxs-lookup"><span data-stu-id="83d32-222">Suppose you need to make a branch – you can do that in Visual Studio too.</span></span> <span data-ttu-id="83d32-223">在**团队资源管理器**中，单击 "**新建分支**"。</span><span class="sxs-lookup"><span data-stu-id="83d32-223">In **Team Explorer**, click **New Branch**.</span></span>

![团队资源管理器新建分支](source-control/_static/image16.png)

<span data-ttu-id="83d32-225">输入分支名称，单击 "**创建分支**"，如果已选择 "**签出分支**"，则 Visual Studio 会自动签出新分支。</span><span class="sxs-lookup"><span data-stu-id="83d32-225">Enter a branch name, click **Create Branch**, and if you selected **Checkout branch**, Visual Studio automatically checks out the new branch.</span></span>

![团队资源管理器新建分支](source-control/_static/image17.png)

<span data-ttu-id="83d32-227">你现在可以对文件进行更改并将其签入此分支。</span><span class="sxs-lookup"><span data-stu-id="83d32-227">You can now make changes to files and check them in to this branch.</span></span> <span data-ttu-id="83d32-228">你可以轻松地在分支之间切换，Visual Studio 会自动将文件同步到已签出的任何分支。在此示例中， *\_布局*中的网页标题已更改为 HotFix1 分支中的 "热修复 1"。</span><span class="sxs-lookup"><span data-stu-id="83d32-228">And you can easily switch between branches and Visual Studio automatically syncs the files to whichever branch you have checked out. In this example the web page title in *\_Layout.cshtml* has been changed to "Hot Fix 1" in HotFix1 branch.</span></span>

![Hotfix1 分支](source-control/_static/image18.png)

<span data-ttu-id="83d32-230">如果切换回 master 分支， *\_的布局. cshtml*文件的内容将自动还原为它们在 master 分支中的内容。</span><span class="sxs-lookup"><span data-stu-id="83d32-230">If you switch back to the master branch, the contents of the *\_Layout.cshtml* file automatically revert to what they are in the master branch.</span></span>

![主分支](source-control/_static/image19.png)

<span data-ttu-id="83d32-232">这是一个简单的示例，演示如何快速创建分支，以及如何在分支之间来回切换。</span><span class="sxs-lookup"><span data-stu-id="83d32-232">This a simple example of how you can quickly create a branch and flip back and forth between branches.</span></span> <span data-ttu-id="83d32-233">此功能使用 "[自动执行所有](automate-everything.md)操作" 一章中介绍的分支结构和自动化脚本，实现了高度敏捷的工作流。</span><span class="sxs-lookup"><span data-stu-id="83d32-233">This feature enables a highly agile workflow using the branch structure and automation scripts presented in the [Automate Everything](automate-everything.md) chapter.</span></span> <span data-ttu-id="83d32-234">例如，你可以在开发分支中工作，从主节点创建热修复分支，切换到新分支，在那里进行更改并提交，然后切换回开发分支，并继续执行所做的操作。</span><span class="sxs-lookup"><span data-stu-id="83d32-234">For example, you can be working in the Development branch, create a hot fix branch off of master, switch to the new branch, make your changes there and commit them, and then switch back to the Development branch and continue what you were doing.</span></span>

<span data-ttu-id="83d32-235">您在这里看到的是如何使用 Visual Studio 中的本地 Git 存储库。</span><span class="sxs-lookup"><span data-stu-id="83d32-235">What you've seen here is how you work with a local Git repository in Visual Studio.</span></span> <span data-ttu-id="83d32-236">在团队环境中，通常还会将更改推送到公共存储库中。</span><span class="sxs-lookup"><span data-stu-id="83d32-236">In a team environment you typically also push changes up to a common repository.</span></span> <span data-ttu-id="83d32-237">使用 Visual Studio 工具还可以指向远程 Git 存储库。</span><span class="sxs-lookup"><span data-stu-id="83d32-237">The Visual Studio tools also enable you to point to a remote Git repository.</span></span> <span data-ttu-id="83d32-238">你可以使用 GitHub.com 来实现此目的，也可以将[Git 和 Azure Repos](/azure/devops/repos/git/overview?view=vsts)与所有其他 Azure DevOps 功能（如工作项和 bug 跟踪）相集成。</span><span class="sxs-lookup"><span data-stu-id="83d32-238">You can use GitHub.com for that purpose, or you can use [Git and Azure Repos](/azure/devops/repos/git/overview?view=vsts) integrated with all the other Azure DevOps capabilities such as work item and bug tracking.</span></span>

<span data-ttu-id="83d32-239">当然，这并不是实现敏捷分支策略的唯一方法。</span><span class="sxs-lookup"><span data-stu-id="83d32-239">This isn't the only way you can implement an agile branching strategy, of course.</span></span> <span data-ttu-id="83d32-240">您可以使用集中式的源代码管理存储库启用相同的敏捷工作流。</span><span class="sxs-lookup"><span data-stu-id="83d32-240">You can enable the same agile workflow using a centralized source control repository.</span></span>

## <a name="summary"></a><span data-ttu-id="83d32-241">总结</span><span class="sxs-lookup"><span data-stu-id="83d32-241">Summary</span></span>

<span data-ttu-id="83d32-242">基于你进行更改的速度，并以安全、可预测的方式，衡量你的源代码管理系统是否成功。</span><span class="sxs-lookup"><span data-stu-id="83d32-242">Measure the success of your source control system based on how quickly you can make a change and get it live in a safe and predictable way.</span></span> <span data-ttu-id="83d32-243">如果你发现自己的恐惧进行了更改，因为你必须对其进行一次或两次手动测试，你可能会问自己必须执行的操作或测试，以便可以在几分钟内或在最糟的时间不超过1小时进行该更改。</span><span class="sxs-lookup"><span data-stu-id="83d32-243">If you find yourself scared to make a change because you have to do a day or two of manual testing on it, you might ask yourself what you have to do process-wise or test-wise so that you can make that change in minutes or at worst no longer than an hour.</span></span> <span data-ttu-id="83d32-244">实现此目的的一种策略是实现持续集成和持续交付，这将在[下一章](continuous-integration-and-continuous-delivery.md)中介绍。</span><span class="sxs-lookup"><span data-stu-id="83d32-244">One strategy for doing that is to implement continuous integration and continuous delivery, which we'll cover in the [next chapter](continuous-integration-and-continuous-delivery.md).</span></span>

<a id="resources"></a>
## <a name="resources"></a><span data-ttu-id="83d32-245">资源</span><span class="sxs-lookup"><span data-stu-id="83d32-245">Resources</span></span>

<span data-ttu-id="83d32-246">有关分支策略的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="83d32-246">For more information about branching strategies, see the following resources:</span></span>

- <span data-ttu-id="83d32-247">[使用 Team Foundation Server 2012 构建发布管道](https://msdn.microsoft.com/library/dn449957.aspx)。</span><span class="sxs-lookup"><span data-stu-id="83d32-247">[Building a Release Pipeline with Team Foundation Server 2012](https://msdn.microsoft.com/library/dn449957.aspx).</span></span> <span data-ttu-id="83d32-248">Microsoft 模式和实践文档。</span><span class="sxs-lookup"><span data-stu-id="83d32-248">Microsoft Patterns and Practices documentation.</span></span> <span data-ttu-id="83d32-249">有关分支策略的讨论，请参阅第6章。</span><span class="sxs-lookup"><span data-stu-id="83d32-249">See chapter 6 for a discussion of branching strategies.</span></span> <span data-ttu-id="83d32-250">拥护者功能会切换功能分支，并且如果使用功能的分支，则会使它们保持短暂生存期（最多小时或天）。</span><span class="sxs-lookup"><span data-stu-id="83d32-250">Advocates feature toggles over feature branches, and if branches for features are used, advocates keeping them short-lived (hours or days at most).</span></span>
- <span data-ttu-id="83d32-251">[版本控制指南](https://aka.ms/vsarsolutions)。</span><span class="sxs-lookup"><span data-stu-id="83d32-251">[Version Control Guide](https://aka.ms/vsarsolutions).</span></span> <span data-ttu-id="83d32-252">ALM Rangers 的分支策略指南。</span><span class="sxs-lookup"><span data-stu-id="83d32-252">Guide to branching strategies by the ALM Rangers.</span></span> <span data-ttu-id="83d32-253">请参阅 "下载" 选项卡上的分支策略。</span><span class="sxs-lookup"><span data-stu-id="83d32-253">See Branching Strategies.pdf on the Downloads tab.</span></span>
- <span data-ttu-id="83d32-254">[通过功能切换进行软件开发](https://msdn.microsoft.com/magazine/dn683796.aspx)。</span><span class="sxs-lookup"><span data-stu-id="83d32-254">[Software Development with Feature Toggles](https://msdn.microsoft.com/magazine/dn683796.aspx).</span></span> <span data-ttu-id="83d32-255">MSDN 杂志文章。</span><span class="sxs-lookup"><span data-stu-id="83d32-255">MSDN Magazine article.</span></span>
- <span data-ttu-id="83d32-256">[功能切换](http://martinfowler.com/bliki/FeatureToggle.html)。</span><span class="sxs-lookup"><span data-stu-id="83d32-256">[Feature Toggle](http://martinfowler.com/bliki/FeatureToggle.html).</span></span> <span data-ttu-id="83d32-257">圣马丁 Fowler 的博客上的功能切换/功能标志简介。</span><span class="sxs-lookup"><span data-stu-id="83d32-257">Introduction to feature toggles / feature flags on Martin Fowler's blog.</span></span>
- <span data-ttu-id="83d32-258">[功能切换 Vs 功能分支](http://geekswithblogs.net/Optikal/archive/2013/02/10/152069.aspx)。</span><span class="sxs-lookup"><span data-stu-id="83d32-258">[Feature Toggles vs Feature Branches](http://geekswithblogs.net/Optikal/archive/2013/02/10/152069.aspx).</span></span> <span data-ttu-id="83d32-259">有关功能的另一篇博客文章 Dylan Smith。</span><span class="sxs-lookup"><span data-stu-id="83d32-259">Another blog post about feature toggles, by Dylan Smith.</span></span>

<span data-ttu-id="83d32-260">有关如何处理不应保留在源代码管理存储库中的敏感信息的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="83d32-260">For more information about how to handle sensitive information that should not be kept in source control repositories, see the following resources:</span></span>

- <span data-ttu-id="83d32-261">[将密码和其他敏感数据部署到 ASP.NET 和 Azure App Service 的最佳实践](../../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="83d32-261">[Best practices for deploying passwords and other sensitive data to ASP.NET and Azure App Service](../../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span></span>
- <span data-ttu-id="83d32-262">[Azure 网站：应用程序字符串和连接字符串的工作原理](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/)。</span><span class="sxs-lookup"><span data-stu-id="83d32-262">[Azure Web Sites: How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span></span> <span data-ttu-id="83d32-263">说明替代*web.config*文件中 `appSettings` 和 `connectionStrings` 数据的 Azure 功能。</span><span class="sxs-lookup"><span data-stu-id="83d32-263">Explains the Azure feature that overrides `appSettings` and `connectionStrings` data in the *Web.config* file.</span></span>
- <span data-ttu-id="83d32-264">[Azure 网站中的自定义配置和应用程序设置-具有 Stefan Schackow](https://azure.microsoft.com/documentation/videos/configuration-and-app-settings-of-azure-web-sites/)。</span><span class="sxs-lookup"><span data-stu-id="83d32-264">[Custom configuration and application settings in Azure Web Sites - with Stefan Schackow](https://azure.microsoft.com/documentation/videos/configuration-and-app-settings-of-azure-web-sites/).</span></span>

<span data-ttu-id="83d32-265">有关将敏感信息保留在源代码管理之外的其他方法的信息，请参阅[ASP.NET MVC：将专用设置保留在源代码管理之外](http://typecastexception.com/post/2014/04/06/ASPNET-MVC-Keep-Private-Settings-Out-of-Source-Control.aspx)。</span><span class="sxs-lookup"><span data-stu-id="83d32-265">For information about other methods for keeping sensitive information out of source control, see [ASP.NET MVC: Keep Private Settings Out of Source Control](http://typecastexception.com/post/2014/04/06/ASPNET-MVC-Keep-Private-Settings-Out-of-Source-Control.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="83d32-266">[上一页](automate-everything.md)
> [下一页](continuous-integration-and-continuous-delivery.md)</span><span class="sxs-lookup"><span data-stu-id="83d32-266">[Previous](automate-everything.md)
[Next](continuous-integration-and-continuous-delivery.md)</span></span>
