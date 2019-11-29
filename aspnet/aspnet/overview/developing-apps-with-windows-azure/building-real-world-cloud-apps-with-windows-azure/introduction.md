---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
title: 用 Azure 构建实际的云应用 |Microsoft Docs
author: MikeWasson
description: 此电子书指导你完成构建真实云解决方案的基于模式的方法。 这些模式适用于开发流程以及 。
ms.author: riande
ms.date: 06/12/2014
ms.assetid: accfa16a-ab15-4c26-9ad4-babdc2a77d2e
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
msc.type: authoredcontent
ms.openlocfilehash: 8a4ef3aa37a9296e92fbeb513968e3abeee072d0
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74585520"
---
# <a name="building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="a7809-104">用 Azure 构建实际的云应用</span><span class="sxs-lookup"><span data-stu-id="a7809-104">Building Real-World Cloud Apps with Azure</span></span>

<span data-ttu-id="a7809-105">作者： [Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson]((https://twitter.com/RickAndMSFT))， [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="a7809-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="a7809-106">[下载 Fix It 项目](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="a7809-106">[Download Fix It Project](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) or [Download E-book](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span></span>

> <span data-ttu-id="a7809-107">此电子书指导你完成构建真实云解决方案的基于模式的方法。</span><span class="sxs-lookup"><span data-stu-id="a7809-107">This e-book walks you through a patterns-based approach to building real-world cloud solutions.</span></span> <span data-ttu-id="a7809-108">模式适用于开发流程以及体系结构和编码实践。</span><span class="sxs-lookup"><span data-stu-id="a7809-108">The patterns apply to the development process as well as to architecture and coding practices.</span></span>
> 
> <span data-ttu-id="a7809-109">内容基于 Scott Guthrie 开发的演示文稿，他在2013年6月（[第 1](http://vimeo.com/68215538)部分、[第 2](http://vimeo.com/68215602)部分）和年 9 2013[月（第一部分，第](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR324) [2](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR325)部分）的 Microsoft Tech ED 澳大利亚的挪威开发人员大会（NDC）举行。</span><span class="sxs-lookup"><span data-stu-id="a7809-109">The content is based on a presentation developed by Scott Guthrie and delivered by him at the Norwegian Developers Conference (NDC) in June of 2013 ([part 1](http://vimeo.com/68215538), [part 2](http://vimeo.com/68215602)), and at Microsoft Tech Ed Australia in September, 2013 ([part 1](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR324), [part 2](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR325)).</span></span> <span data-ttu-id="a7809-110">[许多人](more-patterns-and-guidance.md#acknowledgments)在将内容从视频转换为书面形式时更新并增加了内容。</span><span class="sxs-lookup"><span data-stu-id="a7809-110">[Many others](more-patterns-and-guidance.md#acknowledgments) updated and augmented the content while transitioning it from video to written form.</span></span>

## <a name="intended-audience"></a><span data-ttu-id="a7809-111">目标受众</span><span class="sxs-lookup"><span data-stu-id="a7809-111">Intended Audience</span></span>

<span data-ttu-id="a7809-112">如果开发人员想要了解如何针对云进行开发（考虑迁移到云），或者是云开发新手，则可以从这里简要概述他们需要知道的最重要概念和实践。</span><span class="sxs-lookup"><span data-stu-id="a7809-112">Developers who are curious about developing for the cloud, considering a move to the cloud, or are new to cloud development will find here a concise overview of the most important concepts and practices they need to know.</span></span> <span data-ttu-id="a7809-113">概念以具体的示例为例，每个章节链接到其他资源以获取更深入的信息。</span><span class="sxs-lookup"><span data-stu-id="a7809-113">The concepts are illustrated with concrete examples, and each chapter links to other resources for more in-depth information.</span></span> <span data-ttu-id="a7809-114">示例和指向其他资源的链接适用于 Microsoft 框架和服务，但阐释的原则也适用于其他 web 开发框架和云环境。</span><span class="sxs-lookup"><span data-stu-id="a7809-114">The examples and the links to additional resources are for Microsoft frameworks and services, but the principles illustrated apply to other web development frameworks and cloud environments as well.</span></span>

<span data-ttu-id="a7809-115">已为云开发的开发人员可能会在此处找到一些建议，使其更成功。</span><span class="sxs-lookup"><span data-stu-id="a7809-115">Developers who are already developing for the cloud may find ideas here that will help make them more successful.</span></span> <span data-ttu-id="a7809-116">可以单独读取系列中的每一章，以便选择感兴趣的主题。</span><span class="sxs-lookup"><span data-stu-id="a7809-116">Each chapter in the series can be read independently, so you can pick and choose topics that you're interested in.</span></span>

<span data-ttu-id="a7809-117">观看 Scott Guthrie 的任何人都可以*通过 Azure 演示来构建真实的云应用*，并希望获得更多详细信息和更新的信息。</span><span class="sxs-lookup"><span data-stu-id="a7809-117">Anyone who watched Scott Guthrie's *Building Real World Cloud Apps with Azure* presentation and wants more details and updated information will find that here.</span></span>

<a id="patterns"></a>
## <a name="cloud-development-patterns"></a><span data-ttu-id="a7809-118">云开发模式</span><span class="sxs-lookup"><span data-stu-id="a7809-118">Cloud development patterns</span></span>

<span data-ttu-id="a7809-119">本电子书介绍了适用于云开发的十三种建议模式。</span><span class="sxs-lookup"><span data-stu-id="a7809-119">This e-book explains thirteen recommended patterns for cloud development.</span></span> <span data-ttu-id="a7809-120">此处使用 "模式" 是一种很大的意义，这意味着建议使用此方法完成操作：开发、设计和编码云应用的最佳方式。</span><span class="sxs-lookup"><span data-stu-id="a7809-120">"Pattern" is used here in a broad sense to mean a recommended way to do things: how best to go about developing, designing, and coding cloud apps.</span></span> <span data-ttu-id="a7809-121">这是一种关键模式，可帮助你 "成功进入成功"，前提是你跟随它们。</span><span class="sxs-lookup"><span data-stu-id="a7809-121">These are key patterns which will help you "fall into the pit of success" if you follow them.</span></span>

- <span data-ttu-id="a7809-122">[自动执行所有](automate-everything.md)操作。</span><span class="sxs-lookup"><span data-stu-id="a7809-122">[Automate everything](automate-everything.md).</span></span>

    - <span data-ttu-id="a7809-123">使用脚本可最大程度地提高效率，并最大程度地减少重复过程中的</span><span class="sxs-lookup"><span data-stu-id="a7809-123">Use scripts to maximize efficiency and minimize errors in repetitive processes.</span></span>
    - <span data-ttu-id="a7809-124">演示： Azure 管理脚本。</span><span class="sxs-lookup"><span data-stu-id="a7809-124">Demo: Azure management scripts.</span></span>
- <span data-ttu-id="a7809-125">[源代码管理](source-control.md)。</span><span class="sxs-lookup"><span data-stu-id="a7809-125">[Source control](source-control.md).</span></span> 

    - <span data-ttu-id="a7809-126">在源代码管理中设置分支结构，以便于 DevOps 工作流。</span><span class="sxs-lookup"><span data-stu-id="a7809-126">Set up branching structure in source control to facilitate DevOps workflow.</span></span>
    - <span data-ttu-id="a7809-127">演示：向源代码管理添加脚本。</span><span class="sxs-lookup"><span data-stu-id="a7809-127">Demo: add scripts to source control.</span></span>
    - <span data-ttu-id="a7809-128">演示：使敏感数据不受源代码管理。</span><span class="sxs-lookup"><span data-stu-id="a7809-128">Demo: keep sensitive data out of source control.</span></span>
    - <span data-ttu-id="a7809-129">演示：在 Visual Studio 中使用 Git。</span><span class="sxs-lookup"><span data-stu-id="a7809-129">Demo: use Git in Visual Studio.</span></span>
- <span data-ttu-id="a7809-130">[持续集成和交付](continuous-integration-and-continuous-delivery.md)。</span><span class="sxs-lookup"><span data-stu-id="a7809-130">[Continuous integration and delivery](continuous-integration-and-continuous-delivery.md).</span></span> 

    - <span data-ttu-id="a7809-131">通过每个源代码管理签入自动完成生成和部署。</span><span class="sxs-lookup"><span data-stu-id="a7809-131">Automate build and deployment with each source control check-in.</span></span>
- <span data-ttu-id="a7809-132">[Web 开发最佳实践](web-development-best-practices.md)。</span><span class="sxs-lookup"><span data-stu-id="a7809-132">[Web development best practices](web-development-best-practices.md).</span></span> 

    - <span data-ttu-id="a7809-133">使 web 层保持无状态。</span><span class="sxs-lookup"><span data-stu-id="a7809-133">Keep web tier stateless.</span></span>
    - <span data-ttu-id="a7809-134">演示：在 Azure App Service 中的 Web 应用中缩放和自动缩放。</span><span class="sxs-lookup"><span data-stu-id="a7809-134">Demo: scaling and auto-scaling in Web Apps in Azure App Service.</span></span>
    - <span data-ttu-id="a7809-135">避免会话状态。</span><span class="sxs-lookup"><span data-stu-id="a7809-135">Avoid session state.</span></span>
    - <span data-ttu-id="a7809-136">在 CDN 不可用时，将 CDN 与回退配合使用。</span><span class="sxs-lookup"><span data-stu-id="a7809-136">Use a CDN with a fallback when the CDN is unavailable.</span></span>
    - <span data-ttu-id="a7809-137">使用异步编程模型。</span><span class="sxs-lookup"><span data-stu-id="a7809-137">Use asynchronous programming model.</span></span>
    - <span data-ttu-id="a7809-138">演示： ASP.NET MVC 和实体框架中的异步。</span><span class="sxs-lookup"><span data-stu-id="a7809-138">Demo: async in ASP.NET MVC and Entity Framework.</span></span>
- <span data-ttu-id="a7809-139">[单一登录](single-sign-on.md)。</span><span class="sxs-lookup"><span data-stu-id="a7809-139">[Single sign-on](single-sign-on.md).</span></span> 

    - <span data-ttu-id="a7809-140">Azure Active Directory 简介。</span><span class="sxs-lookup"><span data-stu-id="a7809-140">Introduction to Azure Active Directory.</span></span>
    - <span data-ttu-id="a7809-141">演示：创建使用 Azure Active Directory 的 ASP.NET 应用。</span><span class="sxs-lookup"><span data-stu-id="a7809-141">Demo: create an ASP.NET app that uses Azure Active Directory.</span></span>
- <span data-ttu-id="a7809-142">[数据存储选项](data-storage-options.md)。</span><span class="sxs-lookup"><span data-stu-id="a7809-142">[Data storage options](data-storage-options.md).</span></span> 

    - <span data-ttu-id="a7809-143">数据存储区的类型。</span><span class="sxs-lookup"><span data-stu-id="a7809-143">Types of data stores.</span></span>
    - <span data-ttu-id="a7809-144">如何选择正确的数据存储。</span><span class="sxs-lookup"><span data-stu-id="a7809-144">How to choose the right data store.</span></span>
    - <span data-ttu-id="a7809-145">演示： Azure SQL 数据库。</span><span class="sxs-lookup"><span data-stu-id="a7809-145">Demo: Azure SQL Database.</span></span>
- <span data-ttu-id="a7809-146">[数据分区策略](data-partitioning-strategies.md)。</span><span class="sxs-lookup"><span data-stu-id="a7809-146">[Data partitioning strategies](data-partitioning-strategies.md).</span></span> 

    - <span data-ttu-id="a7809-147">将数据垂直和/或水平分区，以便于缩放关系数据库。</span><span class="sxs-lookup"><span data-stu-id="a7809-147">Partition data vertically, horizontally, or both to facilitate scaling a relational database.</span></span>
- <span data-ttu-id="a7809-148">[非结构化 blob 存储](unstructured-blob-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="a7809-148">[Unstructured blob storage](unstructured-blob-storage.md).</span></span> 

    - <span data-ttu-id="a7809-149">使用 blob 服务在云中存储文件。</span><span class="sxs-lookup"><span data-stu-id="a7809-149">Store files in the cloud by using the blob service.</span></span>
    - <span data-ttu-id="a7809-150">演示：在 Fix It 应用中使用 blob 存储。</span><span class="sxs-lookup"><span data-stu-id="a7809-150">Demo: using blob storage in the Fix It app.</span></span>
- <span data-ttu-id="a7809-151">[设计为可经受故障](design-to-survive-failures.md)。</span><span class="sxs-lookup"><span data-stu-id="a7809-151">[Design to survive failures](design-to-survive-failures.md).</span></span> 

    - <span data-ttu-id="a7809-152">故障类型。</span><span class="sxs-lookup"><span data-stu-id="a7809-152">Types of failures.</span></span>
    - <span data-ttu-id="a7809-153">故障范围。</span><span class="sxs-lookup"><span data-stu-id="a7809-153">Failure Scope.</span></span>
    - <span data-ttu-id="a7809-154">了解 Sla。</span><span class="sxs-lookup"><span data-stu-id="a7809-154">Understanding SLAs.</span></span>
- <span data-ttu-id="a7809-155">[监视和遥测](monitoring-and-telemetry.md)。</span><span class="sxs-lookup"><span data-stu-id="a7809-155">[Monitoring and telemetry](monitoring-and-telemetry.md).</span></span> 

    - <span data-ttu-id="a7809-156">为什么您应该购买一个遥测应用程序并编写自己的代码来检测您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="a7809-156">Why you should both buy a telemetry app and write your own code to instrument your app.</span></span>
    - <span data-ttu-id="a7809-157">演示： Azure 的新 Relic</span><span class="sxs-lookup"><span data-stu-id="a7809-157">Demo: New Relic for Azure</span></span>
    - <span data-ttu-id="a7809-158">演示：在 Fix It 应用中记录代码。</span><span class="sxs-lookup"><span data-stu-id="a7809-158">Demo: logging code in the Fix It app.</span></span>
    - <span data-ttu-id="a7809-159">演示： Fix It 应用中的依赖关系注入。</span><span class="sxs-lookup"><span data-stu-id="a7809-159">Demo: dependency injection in the Fix It app.</span></span>
    - <span data-ttu-id="a7809-160">演示：在 Azure 中提供内置日志记录支持。</span><span class="sxs-lookup"><span data-stu-id="a7809-160">Demo: built-in logging support in Azure.</span></span>
- <span data-ttu-id="a7809-161">[暂时性故障处理](transient-fault-handling.md)。</span><span class="sxs-lookup"><span data-stu-id="a7809-161">[Transient fault handling](transient-fault-handling.md).</span></span> 

    - <span data-ttu-id="a7809-162">使用智能重试/回退逻辑来缓解暂时性故障的影响。</span><span class="sxs-lookup"><span data-stu-id="a7809-162">Use smart retry/back-off logic to mitigate the effect of transient failures.</span></span>
    - <span data-ttu-id="a7809-163">演示：在实体框架6中重试/后退。</span><span class="sxs-lookup"><span data-stu-id="a7809-163">Demo: retry/back-off in Entity Framework 6.</span></span>
- <span data-ttu-id="a7809-164">[分布式缓存](distributed-caching.md)。</span><span class="sxs-lookup"><span data-stu-id="a7809-164">[Distributed caching](distributed-caching.md).</span></span> 

    - <span data-ttu-id="a7809-165">使用分布式缓存提高可伸缩性并降低数据库事务成本。</span><span class="sxs-lookup"><span data-stu-id="a7809-165">Improve scalability and reduce database transaction costs by using distributed caching.</span></span>
- <span data-ttu-id="a7809-166">以[队列为中心的工作模式](queue-centric-work-pattern.md)。</span><span class="sxs-lookup"><span data-stu-id="a7809-166">[Queue-centric work pattern](queue-centric-work-pattern.md).</span></span> 

    - <span data-ttu-id="a7809-167">实现高可用性，并通过松散耦合 web 和辅助角色层提高可伸缩性。</span><span class="sxs-lookup"><span data-stu-id="a7809-167">Enable high availability and improve scalability by loosely coupling web and worker tiers.</span></span>
    - <span data-ttu-id="a7809-168">演示： Fix It 应用中的 Azure 存储队列。</span><span class="sxs-lookup"><span data-stu-id="a7809-168">Demo: Azure storage queues in the Fix It app.</span></span>
- <span data-ttu-id="a7809-169">[更多云应用模式和指南](more-patterns-and-guidance.md)。</span><span class="sxs-lookup"><span data-stu-id="a7809-169">[More cloud app patterns and guidance](more-patterns-and-guidance.md).</span></span>
- [<span data-ttu-id="a7809-170">附录：“Fix It”示例应用程序</span><span class="sxs-lookup"><span data-stu-id="a7809-170">Appendix: The Fix It Sample Application</span></span>](the-fix-it-sample-application.md)

    - <span data-ttu-id="a7809-171">已知问题</span><span class="sxs-lookup"><span data-stu-id="a7809-171">Known Issues</span></span>
    - <span data-ttu-id="a7809-172">最佳做法</span><span class="sxs-lookup"><span data-stu-id="a7809-172">Best Practices</span></span>
    - <span data-ttu-id="a7809-173">如何下载、构建、运行和部署。</span><span class="sxs-lookup"><span data-stu-id="a7809-173">How to download, build, run, and deploy.</span></span>

<span data-ttu-id="a7809-174">这些模式适用于所有云环境，但我们将使用基于 Microsoft 技术和服务（如 Visual Studio、Team Foundation Service、ASP.NET 和 Azure）的示例来演示这些模式。</span><span class="sxs-lookup"><span data-stu-id="a7809-174">These patterns apply to all cloud environments, but we'll illustrate them by using examples based on Microsoft technologies and services, such as Visual Studio, Team Foundation Service, ASP.NET, and Azure.</span></span>

<span data-ttu-id="a7809-175">本章的其余部分介绍了 fix it 示例应用程序和 Web 应用在 Azure App Service 的云环境中运行。</span><span class="sxs-lookup"><span data-stu-id="a7809-175">This remainder of this chapter introduces the Fix It sample application and the Web Apps in Azure App Service cloud environment that the Fix It app runs in.</span></span>

<a id="fixit"></a>
## <a name="the-fix-it-sample-application"></a><span data-ttu-id="a7809-176">Fix it 示例应用程序</span><span class="sxs-lookup"><span data-stu-id="a7809-176">The Fix it sample application</span></span>

<span data-ttu-id="a7809-177">本电子书中所示的大部分屏幕截图和代码示例都基于[Scott Guthrie](https://weblogs.asp.net/scottgu/)最初开发的 Fix It 应用，旨在演示推荐的云应用开发模式和实践。</span><span class="sxs-lookup"><span data-stu-id="a7809-177">Most of the screen shots and code examples shown in this e-book are based on the Fix It app originally developed by [Scott Guthrie](https://weblogs.asp.net/scottgu/) to demonstrate recommended cloud app development patterns and practices.</span></span>

![Fix It 应用主页](introduction/_static/image1.png)

<span data-ttu-id="a7809-179">该示例应用程序是一个简单的工作项票证系统。</span><span class="sxs-lookup"><span data-stu-id="a7809-179">The sample app is a simple work item ticketing system.</span></span> <span data-ttu-id="a7809-180">当你需要固定的内容时，你可以创建一个票证并将其分配给某人，其他人可以登录并查看分配给他们的票证，并在完成工作后将票证标记为已完成。</span><span class="sxs-lookup"><span data-stu-id="a7809-180">When you need something fixed, you create a ticket and assign it to someone, and others can log in and see the tickets assigned to them and mark tickets as completed when the work is done.</span></span>

<span data-ttu-id="a7809-181">这是标准的 Visual Studio web 项目。</span><span class="sxs-lookup"><span data-stu-id="a7809-181">It's a standard Visual Studio web project.</span></span> <span data-ttu-id="a7809-182">它基于 ASP.NET MVC 构建并使用 SQL Server 数据库。</span><span class="sxs-lookup"><span data-stu-id="a7809-182">It is built on ASP.NET MVC and uses a SQL Server database.</span></span> <span data-ttu-id="a7809-183">它可以在 IIS Express 本地运行，并且可以部署到 Azure 网站以在云中运行。</span><span class="sxs-lookup"><span data-stu-id="a7809-183">It can run locally in IIS Express and can be deployed to a Azure Web Site to run in the cloud.</span></span> <span data-ttu-id="a7809-184">您可以使用窗体身份验证和本地数据库或使用社交提供程序（如 Google）登录。</span><span class="sxs-lookup"><span data-stu-id="a7809-184">You can log in using forms authentication and a local database or by using a social provider such as Google.</span></span> <span data-ttu-id="a7809-185">（稍后我们还将演示如何使用 Active Directory 组织帐户进行登录。）</span><span class="sxs-lookup"><span data-stu-id="a7809-185">(Later we'll also show how to log in with an Active Directory organizational account.)</span></span>

![登录页](introduction/_static/image2.png)

<span data-ttu-id="a7809-187">登录后，可以创建票证，将其分配给某人，并上传要修复的内容的图片。</span><span class="sxs-lookup"><span data-stu-id="a7809-187">Once you're logged in you can create a ticket, assign it to someone, and upload a picture of what you want to get fixed.</span></span>

![创建 Fix It 任务](introduction/_static/image3.png)

![已创建修复 It 任务](introduction/_static/image4.png)

<span data-ttu-id="a7809-190">你可以跟踪创建的工作项的进度，查看分配给你的票证，查看票证详细信息，并将项标记为已完成。</span><span class="sxs-lookup"><span data-stu-id="a7809-190">You can track the progress of work items you created, see tickets assigned to you, view ticket details, and mark items as completed.</span></span>

<span data-ttu-id="a7809-191">这是一个非常简单的应用程序，从功能角度看，您将了解如何生成该应用程序，以便它可以扩展到数百万的用户，并且可以灵活应对数据库故障和连接终止等因素。</span><span class="sxs-lookup"><span data-stu-id="a7809-191">This is a very simple app from a feature perspective, but you'll see how to build it so that it can scale to millions of users and will be resilient to things like database failures and connection terminations.</span></span> <span data-ttu-id="a7809-192">你还将了解如何创建自动化的敏捷开发工作流，该工作流可让你轻松、快速地循环访问开发周期，使应用更好、更好地实现。</span><span class="sxs-lookup"><span data-stu-id="a7809-192">You'll also see how to create an automated and agile development workflow, which enables you to start simple and make the app better and better by iterating the development cycle efficiently and quickly.</span></span>

<a id="waws"></a>
## <a name="web-apps-in-azure-app-service"></a><span data-ttu-id="a7809-193">Azure App Service 中的 Web 应用</span><span class="sxs-lookup"><span data-stu-id="a7809-193">Web Apps in Azure App Service</span></span>

<span data-ttu-id="a7809-194">用于 Fix It 应用程序的云环境是 Azure 的一种服务，我们称之为 "网站"。</span><span class="sxs-lookup"><span data-stu-id="a7809-194">The cloud environment used for the Fix It application is a service of Azure that we call Web Sites.</span></span> <span data-ttu-id="a7809-195">此服务是一种可在 Azure 中托管自己的 web 应用的方法，无需创建 Vm，并使其保持更新、安装和配置 IIS 等。我们将网站托管在 Vm 上，并自动为你提供备份和恢复及其他服务。</span><span class="sxs-lookup"><span data-stu-id="a7809-195">This service is a way that you can host your own web app in Azure without having to create VMs and keep them updated, install and configure IIS, etc. We host your site on our VMs and automatically provide backup and recovery and other services for you.</span></span> <span data-ttu-id="a7809-196">网站服务适用于 ASP.NET、node.js、PHP 和 Python。</span><span class="sxs-lookup"><span data-stu-id="a7809-196">The Web Sites service works with ASP.NET, Node.js, PHP, and Python.</span></span> <span data-ttu-id="a7809-197">利用它，你可以使用 Visual Studio、Web 部署、FTP、Git 或 TFS 快速进行部署。</span><span class="sxs-lookup"><span data-stu-id="a7809-197">It enables you to deploy very quickly using Visual Studio, Web Deploy, FTP, Git, or TFS.</span></span> <span data-ttu-id="a7809-198">通常只需几秒钟即可开始部署，以及通过 Internet 进行更新的时间。</span><span class="sxs-lookup"><span data-stu-id="a7809-198">It's usually just a few seconds between the time you start a deployment and the time your update is available over the Internet.</span></span> <span data-ttu-id="a7809-199">这一切都是免费的，可以在流量增长时进行扩展。</span><span class="sxs-lookup"><span data-stu-id="a7809-199">It's all free to get started, and you can scale up as your traffic grows.</span></span>

<span data-ttu-id="a7809-200">在幕后，Azure App Service 中的 Web 应用程序提供了大量体系结构组件和功能，如果您打算在自己的 Vm 上使用 IIS 来承载网站，则必须自行构建。</span><span class="sxs-lookup"><span data-stu-id="a7809-200">Behind the scenes, Web Apps in Azure App Service provides a lot of architectural components and features that you'd have to build yourself if you were going to host a web site using IIS on your own VMs.</span></span> <span data-ttu-id="a7809-201">一个组件是自动配置 IIS 的部署终结点，并将你的应用程序安装到你想要在其上运行站点的任意多个 Vm 上。</span><span class="sxs-lookup"><span data-stu-id="a7809-201">One component is a deployment end point that automatically configures IIS and installs your application on as many VMs as you want to run your site on.</span></span>

![部署服务](introduction/_static/image5.png)

<span data-ttu-id="a7809-203">当用户访问该网站时，他们不会直接命中 IIS Vm，而是通过[应用程序请求路由（ARR）](https://www.iis.net/downloads/microsoft/application-request-routing)负载平衡器。</span><span class="sxs-lookup"><span data-stu-id="a7809-203">When a user hits the web site, they don't hit the IIS VMs directly, they go through [Application Request Routing (ARR)](https://www.iis.net/downloads/microsoft/application-request-routing) load balancers.</span></span> <span data-ttu-id="a7809-204">您可以将这些服务器与自己的服务器一起使用，但此处的优点是它们会自动设置。</span><span class="sxs-lookup"><span data-stu-id="a7809-204">You can use these with your own servers, but the advantage here is that they're set up for you automatically.</span></span> <span data-ttu-id="a7809-205">它们使用智能试探法，其中包括会话相关性、IIS 中的队列深度和每台计算机上的 CPU 使用率等因素，以将流量定向到托管您的网站的虚拟机。</span><span class="sxs-lookup"><span data-stu-id="a7809-205">They use a smart heuristic that takes into account factors such as session affinity, queue depth in IIS, and CPU usage on each machine to direct traffic to the VMs that host your web site.</span></span>

![ARR 负载均衡器](introduction/_static/image6.png)

<span data-ttu-id="a7809-207">如果某个计算机出现故障，Azure 会自动从轮换中提取该虚拟机，并启动新的 VM 实例，并开始将流量定向到新的实例-所有应用程序都不会停机。</span><span class="sxs-lookup"><span data-stu-id="a7809-207">If a machine goes down, Azure automatically pulls it from the rotation, spins up a new VM instance, and starts directing traffic to the new instance -- all with no down time for your application.</span></span>

![从计算机故障中自动恢复](introduction/_static/image7.png)

<span data-ttu-id="a7809-209">这一切都是自动进行的。</span><span class="sxs-lookup"><span data-stu-id="a7809-209">All of this takes place automatically.</span></span> <span data-ttu-id="a7809-210">只需创建一个网站并使用 Windows PowerShell、Visual Studio 或 Azure 管理门户将应用程序部署到该网站。</span><span class="sxs-lookup"><span data-stu-id="a7809-210">All you need to do is create a web site and deploy your application to it, using Windows PowerShell, Visual Studio, or the Azure management portal.</span></span>

<span data-ttu-id="a7809-211">有关演示如何在 Visual Studio 中创建 web 应用程序并将其部署到 Azure 网站的快捷快捷教程，请参阅[Azure 和 ASP.NET 入门](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)。</span><span class="sxs-lookup"><span data-stu-id="a7809-211">For a quick and easy step-by-step tutorial that shows how to create a web application in Visual Studio and deploy it to a Azure Web Site, see [Get started with Azure and ASP.NET](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/).</span></span>

<a id="summary"></a>
## <a name="summary"></a><span data-ttu-id="a7809-212">总结</span><span class="sxs-lookup"><span data-stu-id="a7809-212">Summary</span></span>

<span data-ttu-id="a7809-213">本简介提供了本书将介绍的主题的列表、示例应用程序的屏幕截图，以及 Azure App Service 云环境中的 Web 应用程序的简要概述。</span><span class="sxs-lookup"><span data-stu-id="a7809-213">This introduction has provided a list of topics the book will cover, screenshots of the sample application, and a brief overview of the Web Apps in Azure App Service cloud environment.</span></span> <span data-ttu-id="a7809-214">在和中开发应用程序的一个很好的优点是，可以轻松地自动执行重复的开发任务，如创建测试环境并向其部署代码。</span><span class="sxs-lookup"><span data-stu-id="a7809-214">One of the great advantages of developing apps in and for the cloud is that it's easy to automate repetitive development tasks such as creating a test environment and deploying your code to it.</span></span> <span data-ttu-id="a7809-215">如何执行此操作是[下一章](automate-everything.md)的主题。</span><span class="sxs-lookup"><span data-stu-id="a7809-215">How to do that is the subject of the [next chapter](automate-everything.md).</span></span>

## <a name="resources"></a><span data-ttu-id="a7809-216">资源</span><span class="sxs-lookup"><span data-stu-id="a7809-216">Resources</span></span>

<span data-ttu-id="a7809-217">有关本章所涵盖主题的详细信息，请参阅以下资源。</span><span class="sxs-lookup"><span data-stu-id="a7809-217">For more information about the topics covered in this chapter, see the following resources.</span></span>

<span data-ttu-id="a7809-218">文档：</span><span class="sxs-lookup"><span data-stu-id="a7809-218">Documentation:</span></span>

- <span data-ttu-id="a7809-219">[Azure App Service 中的 Web 应用](https://azure.microsoft.com/services/app-service/web/)。</span><span class="sxs-lookup"><span data-stu-id="a7809-219">[Web Apps in Azure App Service](https://azure.microsoft.com/services/app-service/web/).</span></span> <span data-ttu-id="a7809-220">有关 Web 应用的 Azure 文档的门户页。</span><span class="sxs-lookup"><span data-stu-id="a7809-220">Portal page for Azure documentation about Web Apps.</span></span>
- [<span data-ttu-id="a7809-221">Web 应用、云服务和 Vm：何时使用哪些功能？</span><span class="sxs-lookup"><span data-stu-id="a7809-221">Web Apps, Cloud Services, and VMs: When to use which?</span></span>](https://azure.microsoft.com/documentation/articles/choose-web-site-cloud-service-vm/) <span data-ttu-id="a7809-222">如 WAWS 所示，只是在 Azure 中运行 web 应用的三种方法之一。</span><span class="sxs-lookup"><span data-stu-id="a7809-222">WAWS as shown in this chapter is just one of three ways you can run web apps in Azure.</span></span> <span data-ttu-id="a7809-223">本文介绍三种方法之间的差异，并提供有关如何选择适合你的方案的指南。</span><span class="sxs-lookup"><span data-stu-id="a7809-223">This article explains the differences between the three ways and gives guidance on how to choose which one is right for your scenario.</span></span> <span data-ttu-id="a7809-224">与网站一样，云服务是 Azure 的一项 PaaS 功能。</span><span class="sxs-lookup"><span data-stu-id="a7809-224">Like Web Sites, Cloud Services is a PaaS feature of Azure.</span></span> <span data-ttu-id="a7809-225">Vm 是 IaaS 功能。</span><span class="sxs-lookup"><span data-stu-id="a7809-225">VMs are an IaaS feature.</span></span> <span data-ttu-id="a7809-226">有关 PaaS 和 IaaS 的说明，请参阅 "[数据选项](data-storage-options.md#paasiaas)" 一章。</span><span class="sxs-lookup"><span data-stu-id="a7809-226">For an explanation of PaaS versus IaaS, see the [Data Options](data-storage-options.md#paasiaas) chapter.</span></span>

<span data-ttu-id="a7809-227">视频：</span><span class="sxs-lookup"><span data-stu-id="a7809-227">Videos:</span></span>

- [<span data-ttu-id="a7809-228">Scott Guthrie 从步骤0开始-什么是 Azure 云 OS？</span><span class="sxs-lookup"><span data-stu-id="a7809-228">Scott Guthrie starts at Step 0 - What is the Azure Cloud OS?</span></span>](https://azure.microsoft.com/documentation/videos/what-is-the-cloud-os-scottgu/)
- <span data-ttu-id="a7809-229">网站[体系结构-具有 Stefan Schackow](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/)。</span><span class="sxs-lookup"><span data-stu-id="a7809-229">[Web Sites Architecture - with Stefan Schackow](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/).</span></span>
- <span data-ttu-id="a7809-230">[Azure 网站与 Nir Mashkowski 的内部机制](https://channel9.msdn.com/Shows/Web+Camps+TV/Windows-Azure-Web-Sites-Internals-with-Nir-Mashkowski)。</span><span class="sxs-lookup"><span data-stu-id="a7809-230">[Azure Web Sites Internals with Nir Mashkowski](https://channel9.msdn.com/Shows/Web+Camps+TV/Windows-Azure-Web-Sites-Internals-with-Nir-Mashkowski).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="a7809-231">下一页</span><span class="sxs-lookup"><span data-stu-id="a7809-231">Next</span></span>](automate-everything.md)
