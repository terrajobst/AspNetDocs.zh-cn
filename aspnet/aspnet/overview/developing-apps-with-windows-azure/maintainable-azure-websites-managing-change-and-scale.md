---
uid: aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale
title: 动手实验：可维护 Azure 网站：管理更改和缩放 |Microsoft Docs
author: rick-anderson
description: 在此实验室中，了解 Microsoft Azure 如何轻松地构建网站并将其部署到生产环境。
ms.author: riande
ms.date: 07/16/2014
ms.assetid: ecfd0eb4-c4ad-44e6-9db9-a2a66611ff6a
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale
msc.type: authoredcontent
ms.openlocfilehash: c88bae40a8aa092037c0b359ee391acaf161cf10
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78506372"
---
# <a name="hands-on-lab-maintainable-azure-websites-managing-change-and-scale"></a><span data-ttu-id="9b3b3-103">动手实验：可维护 Azure 网站：管理更改和缩放</span><span class="sxs-lookup"><span data-stu-id="9b3b3-103">Hands on Lab: Maintainable Azure Websites: Managing Change and Scale</span></span>

<span data-ttu-id="9b3b3-104">由[Web 训练营团队](https://twitter.com/webcamps)使用</span><span class="sxs-lookup"><span data-stu-id="9b3b3-104">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="9b3b3-105">下载 Web 训练营培训工具包</span><span class="sxs-lookup"><span data-stu-id="9b3b3-105">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

> <span data-ttu-id="9b3b3-106">Microsoft Azure 可以轻松地构建网站并将其部署到生产环境。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-106">Microsoft Azure makes it easy to build and deploy websites to production.</span></span> <span data-ttu-id="9b3b3-107">但当您的应用程序处于活动中时，您就会开始吧！</span><span class="sxs-lookup"><span data-stu-id="9b3b3-107">But you're not done when your application is live, you're just getting started!</span></span> <span data-ttu-id="9b3b3-108">需要处理不断变化的要求、数据库更新、规模等。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-108">You'll need to handle changing requirements, database updates, scale, and more.</span></span> <span data-ttu-id="9b3b3-109">幸运的是，Azure App Service 都包含了一些功能，可帮助您保持站点顺利运行。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-109">Fortunately, Azure App Service has you covered, with plenty of features to help you keep your sites running smoothly.</span></span>
>
> <span data-ttu-id="9b3b3-110">Azure 为任意规模的 web 应用程序提供安全而灵活的开发、部署和扩展选项。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-110">Azure offers secure and flexible development, deployment and scaling options for any size web application.</span></span> <span data-ttu-id="9b3b3-111">利用现有工具创建和部署应用程序，而无需管理基础结构。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-111">Leverage your existing tools to create and deploy applications without the hassle of managing infrastructure.</span></span>
>
> <span data-ttu-id="9b3b3-112">使用最喜欢的开发工具轻松部署创建的内容，以分钟为单位轻松预配生产 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-112">Provision a production web application yourself in minutes by easily deploying content created using your favorite development tool.</span></span> <span data-ttu-id="9b3b3-113">可以直接从源代码管理部署现有网站，支持**Git**、 **GitHub**、 **Bitbucket**、 **TFS**甚至**DropBox**。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-113">You can deploy an existing site directly from source control with support for **Git**, **GitHub**, **Bitbucket**, **TFS**, and even **DropBox**.</span></span> <span data-ttu-id="9b3b3-114">在 Windows 中使用 PowerShell 或在任何 OS 上运行的**CLI**工具中使用**PowerShell**直接从你喜欢的 IDE 或脚本进行部署。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-114">Deploy directly from your favorite IDE or from scripts using **PowerShell** in Windows or **CLI** tools running on any OS.</span></span> <span data-ttu-id="9b3b3-115">部署完成后，使你的网站始终保持最新状态，并支持连续部署。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-115">Once deployed, keep your sites constantly up-to-date with support for continuous deployment.</span></span>
>
> <span data-ttu-id="9b3b3-116">Azure 为任何数据（大或小）提供可缩放、持久的云存储、备份和恢复解决方案。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-116">Azure provides scalable, durable cloud storage, backup, and recovery solutions for any data, big or small.</span></span> <span data-ttu-id="9b3b3-117">将应用程序部署到生产环境时，存储服务（如表、Blob 和 SQL 数据库）可帮助你在云中扩展应用程序。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-117">When deploying applications to a production environment, storage services such as Tables, Blobs and SQL Databases, help you scale your application in the cloud.</span></span>
>
> <span data-ttu-id="9b3b3-118">在 SQL 数据库中，当部署应用程序的新版本时，重要的是使您的生产数据库保持最新。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-118">With SQL Databases, it is important to keep your productive database up-to-date when deploying new versions of your application.</span></span> <span data-ttu-id="9b3b3-119">感谢您**Entity Framework Code First 迁移**，您的数据模型的开发和部署已经过简化，只需几分钟就能更新您的环境。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-119">Thanks to **Entity Framework Code First Migrations**, the development and deployment of your data model has been simplified to update your environments in minutes.</span></span> <span data-ttu-id="9b3b3-120">此动手实验将向你显示在 Microsoft Azure 中将 web 应用部署到生产环境时可能会遇到的不同主题。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-120">This hands-on lab will show you the different topics you could encounter when deploying your web app to production environments in Microsoft Azure.</span></span>
>
> <span data-ttu-id="9b3b3-121">所有示例代码和代码段都包含在 Web 训练营培训工具包中， [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit)提供。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-121">All sample code and snippets are included in the Web Camps Training Kit, available at [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit).</span></span>
>
> <span data-ttu-id="9b3b3-122">若要深入了解本主题，请参阅[利用 Azure 电子书构建实际的云应用](building-real-world-cloud-apps-with-windows-azure/introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-122">For more in-depth coverage of this topic, see the [Building Real-World Cloud Apps with Azure e-book](building-real-world-cloud-apps-with-windows-azure/introduction.md).</span></span>

<a id="Overview"></a>
## <a name="overview"></a><span data-ttu-id="9b3b3-123">概述</span><span class="sxs-lookup"><span data-stu-id="9b3b3-123">Overview</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="9b3b3-124">目标</span><span class="sxs-lookup"><span data-stu-id="9b3b3-124">Objectives</span></span>

<span data-ttu-id="9b3b3-125">在本动手实验中，您将了解如何：</span><span class="sxs-lookup"><span data-stu-id="9b3b3-125">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="9b3b3-126">使用现有模型启用实体框架迁移</span><span class="sxs-lookup"><span data-stu-id="9b3b3-126">Enable Entity Framework Migrations with an existing model</span></span>
- <span data-ttu-id="9b3b3-127">使用实体框架迁移相应地更新对象模型和数据库</span><span class="sxs-lookup"><span data-stu-id="9b3b3-127">Update the object model and database accordingly using Entity Framework Migrations</span></span>
- <span data-ttu-id="9b3b3-128">使用 Git 部署到 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="9b3b3-128">Deploy to Azure App Service using Git</span></span>
- <span data-ttu-id="9b3b3-129">使用 Azure 管理门户回滚到以前的部署</span><span class="sxs-lookup"><span data-stu-id="9b3b3-129">Rollback to a previous deployment using the Azure Management portal</span></span>
- <span data-ttu-id="9b3b3-130">使用 Azure 存储缩放 web 应用</span><span class="sxs-lookup"><span data-stu-id="9b3b3-130">Use Azure Storage to scale a web app</span></span>
- <span data-ttu-id="9b3b3-131">使用 Azure 管理门户配置 web 应用的自动缩放</span><span class="sxs-lookup"><span data-stu-id="9b3b3-131">Configure auto-scaling for a web app using the Azure Management Portal</span></span>
- <span data-ttu-id="9b3b3-132">在 Visual Studio 中创建和配置负载测试项目</span><span class="sxs-lookup"><span data-stu-id="9b3b3-132">Create and configure a load test project in Visual Studio</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="9b3b3-133">系统必备</span><span class="sxs-lookup"><span data-stu-id="9b3b3-133">Prerequisites</span></span>

<span data-ttu-id="9b3b3-134">完成本动手实验需要以下各项：</span><span class="sxs-lookup"><span data-stu-id="9b3b3-134">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="9b3b3-135">Web 或更高版本[的 Visual Studio Express 2013](https://www.microsoft.com/visualstudio/)</span><span class="sxs-lookup"><span data-stu-id="9b3b3-135">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) or greater</span></span>
- [<span data-ttu-id="9b3b3-136">用于 .NET 的 Azure SDK 2。2</span><span class="sxs-lookup"><span data-stu-id="9b3b3-136">Azure SDK for .NET 2.2</span></span>](https://www.microsoft.com/windowsazure/sdk/)
- [<span data-ttu-id="9b3b3-137">GIT 版本控制系统</span><span class="sxs-lookup"><span data-stu-id="9b3b3-137">GIT Version Control System</span></span>](http://git-scm.com/download)
- <span data-ttu-id="9b3b3-138">Microsoft Azure 订阅</span><span class="sxs-lookup"><span data-stu-id="9b3b3-138">A Microsoft Azure subscription</span></span>

    - <span data-ttu-id="9b3b3-139">注册[免费试用版](https://aka.ms/watk-freetrial)</span><span class="sxs-lookup"><span data-stu-id="9b3b3-139">Sign up for a [Free Trial](https://aka.ms/watk-freetrial)</span></span>
    - <span data-ttu-id="9b3b3-140">如果你是 Visual Studio Professional，请 Test Professional、高级或旗舰版（MSDN 或 MSDN 平台订阅者）立即激活你的[msdn 权益](https://aka.ms/watk-msdn)，开始在 Azure 上进行开发和测试</span><span class="sxs-lookup"><span data-stu-id="9b3b3-140">If you are a Visual Studio Professional, Test Professional, Premium or Ultimate with MSDN or MSDN Platforms subscriber, activate your [MSDN benefit](https://aka.ms/watk-msdn) now to start developing and testing on Azure</span></span>
    - <span data-ttu-id="9b3b3-141">[BizSpark](https://aka.ms/watk-bizspark)成员通过其 Visual Studio Ultimate with MSDN 订阅自动获得 Azure 权益</span><span class="sxs-lookup"><span data-stu-id="9b3b3-141">[BizSpark](https://aka.ms/watk-bizspark) members automatically receive the Azure benefit through their Visual Studio Ultimate with MSDN subscriptions</span></span>
    - <span data-ttu-id="9b3b3-142">[Microsoft 合作伙伴网络](https://aka.ms/watk-mpn)Cloud Essentials 计划的成员免费接收每月 Azure 额度</span><span class="sxs-lookup"><span data-stu-id="9b3b3-142">Members of the [Microsoft Partner Network](https://aka.ms/watk-mpn) Cloud Essentials program receive monthly Azure credits at no charge</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="9b3b3-143">安装</span><span class="sxs-lookup"><span data-stu-id="9b3b3-143">Setup</span></span>

<span data-ttu-id="9b3b3-144">若要运行此动手实验中的练习，您需要先设置您的环境。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-144">In order to run the exercises in this hands-on lab, you will need to set up your environment first.</span></span>

1. <span data-ttu-id="9b3b3-145">打开 Windows 资源管理器并浏览到实验室的**源**文件夹。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-145">Open Windows Explorer and browse to the lab's **Source** folder.</span></span>
2. <span data-ttu-id="9b3b3-146">右键单击 " **setup.exe** "，然后选择 "以**管理员身份运行**" 以启动安装过程，该过程将配置环境并安装 Visual Studio code 代码段。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-146">Right-click on **Setup.cmd** and select **Run as administrator** to launch the setup process that will configure your environment and install the Visual Studio code snippets for this lab.</span></span>
3. <span data-ttu-id="9b3b3-147">如果显示“用户帐户控制”对话框，请确认操作以继续。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-147">If the User Account Control dialog is shown, confirm the action to proceed.</span></span>

> [!NOTE]
> <span data-ttu-id="9b3b3-148">确保在运行安装过程之前，您已检查本实验的所有依赖项。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-148">Make sure you have checked all the dependencies for this lab before running the setup.</span></span>

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a><span data-ttu-id="9b3b3-149">使用代码段</span><span class="sxs-lookup"><span data-stu-id="9b3b3-149">Using the Code Snippets</span></span>

<span data-ttu-id="9b3b3-150">在整个实验文档中，将指示您插入代码块。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-150">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="9b3b3-151">为方便起见，此代码的大部分作为 Visual Studio Code 代码段提供，你可以从 Visual Studio 2013 中访问这些代码段，以避免手动添加它。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-151">For your convenience, most of this code is provided as Visual Studio Code Snippets, which you can access from within Visual Studio 2013 to avoid having to add it manually.</span></span>

> [!NOTE]
> <span data-ttu-id="9b3b3-152">每个练习都附带了一个起始解决方案，该解决方案位于练习的 "**开始**" 文件夹中，使您可以单独执行每个练习。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-152">Each exercise is accompanied by a starting solution located in the **Begin** folder of the exercise that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="9b3b3-153">请注意，这些开始解决方案中缺少在练习中添加的代码段，并且在完成此练习之前，可能无法工作。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-153">Please be aware that the code snippets that are added during an exercise are missing from these starting solutions and may not work until you have completed the exercise.</span></span> <span data-ttu-id="9b3b3-154">在练习的源代码中，还会找到一个包含 Visual Studio 解决方案的**结束**文件夹，该解决方案的代码是完成相应练习中的步骤所产生的。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-154">Inside the source code for an exercise, you will also find an **End** folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="9b3b3-155">如果您在演练本动手实验时需要其他帮助，则可以使用这些解决方案作为指南。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-155">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>

---

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="9b3b3-156">练习</span><span class="sxs-lookup"><span data-stu-id="9b3b3-156">Exercises</span></span>

<span data-ttu-id="9b3b3-157">本动手实验包括以下练习：</span><span class="sxs-lookup"><span data-stu-id="9b3b3-157">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="9b3b3-158">使用实体框架迁移</span><span class="sxs-lookup"><span data-stu-id="9b3b3-158">Using Entity Framework Migrations</span></span>](#Exercise1)
2. [<span data-ttu-id="9b3b3-159">将 Web 应用部署到过渡环境</span><span class="sxs-lookup"><span data-stu-id="9b3b3-159">Deploying a Web App to Staging</span></span>](#Exercise2)
3. [<span data-ttu-id="9b3b3-160">在生产环境中执行部署回滚</span><span class="sxs-lookup"><span data-stu-id="9b3b3-160">Performing Deployment Rollback in Production</span></span>](#Exercise3)
4. [<span data-ttu-id="9b3b3-161">使用 Azure 存储进行缩放</span><span class="sxs-lookup"><span data-stu-id="9b3b3-161">Scaling Using Azure Storage</span></span>](#Exercise4)
5. <span data-ttu-id="9b3b3-162">[对 Web 应用使用自动缩放](#Exercise5)（适用于 Visual Studio 2013 旗舰版）</span><span class="sxs-lookup"><span data-stu-id="9b3b3-162">[Using Autoscale for Web Apps](#Exercise5) (Optional for Visual Studio 2013 Ultimate edition)</span></span>

<span data-ttu-id="9b3b3-163">完成本实验的估计时间： **75 分钟**</span><span class="sxs-lookup"><span data-stu-id="9b3b3-163">Estimated time to complete this lab: **75 minutes**</span></span>

> [!NOTE]
> <span data-ttu-id="9b3b3-164">首次启动 Visual Studio 时，必须选择一个预定义的设置集合。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-164">When you first start Visual Studio, you must select one of the predefined settings collections.</span></span> <span data-ttu-id="9b3b3-165">每个预定义的集合都设计为与特定的开发风格相匹配，并确定窗口布局、编辑器行为、IntelliSense 代码段和对话框选项。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-165">Each predefined collection is designed to match a particular development style and determines window layouts, editor behavior, IntelliSense code snippets, and dialog box options.</span></span> <span data-ttu-id="9b3b3-166">此实验室中的过程描述在使用**常规开发设置**集合时，在 Visual Studio 中完成给定任务所需执行的操作。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-166">The procedures in this lab describe the actions necessary to accomplish a given task in Visual Studio when using the **General Development Settings** collection.</span></span> <span data-ttu-id="9b3b3-167">如果为开发环境选择了其他设置集合，则需要考虑的步骤可能会有所不同。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-167">If you choose a different settings collection for your development environment, there may be differences in the steps that you should take into account.</span></span>

<a id="Exercise1"></a>
### <a name="exercise-1-using-entity-framework-migrations"></a><span data-ttu-id="9b3b3-168">练习1：使用实体框架迁移</span><span class="sxs-lookup"><span data-stu-id="9b3b3-168">Exercise 1: Using Entity Framework Migrations</span></span>

<span data-ttu-id="9b3b3-169">开发应用程序时，数据模型可能会随时间而改变。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-169">When you are developing an application, your data model might change over time.</span></span> <span data-ttu-id="9b3b3-170">这些更改可能会影响数据库中的现有模型（如果要创建新的版本），并且必须保持数据库的最新状态，以防出现错误。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-170">These changes could affect the existing model in your database (if you are creating a new version) and it is important to keep your database up-to-date to prevent errors.</span></span>

<span data-ttu-id="9b3b3-171">为了简化模型中对这些更改的跟踪， **Entity Framework Code First 迁移**自动检测与数据库架构比较模型的更改，并生成特定代码来更新数据库，从而创建新*版本*的数据库。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-171">To simplify the tracking of these changes in your model, **Entity Framework Code First Migrations** automatically detect changes comparing your model with the database schema and generates specific code to update your database, creating new *versions* of your database.</span></span>

<span data-ttu-id="9b3b3-172">本练习演示如何为应用程序启用**迁移**，以及如何轻松地检测和生成更改来更新数据库。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-172">This exercise shows you how to enable **Migrations** for your application and how you can easily detect and generate changes to update your databases.</span></span>

<a id="Ex1Task1"></a>
#### <a name="task-1--enabling-migrations"></a><span data-ttu-id="9b3b3-173">任务1–启用迁移</span><span class="sxs-lookup"><span data-stu-id="9b3b3-173">Task 1 – Enabling Migrations</span></span>

<span data-ttu-id="9b3b3-174">在此任务中，您将完成为**书呆子测验**数据库启用**Entity Framework Code First 迁移**的步骤，更改模型并了解这些更改在数据库中的反射方式。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-174">In this task, you will go through the steps of enabling **Entity Framework Code First Migrations** to the **Geek Quiz** database, changing the model and understanding how those changes are reflected in the database.</span></span>

1. <span data-ttu-id="9b3b3-175">打开 Visual Studio，并从**Source\Ex1-UsingEntityFrameworkMigrations\Begin**打开**GeekQuiz**解决方案文件。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-175">Open Visual Studio and open the **GeekQuiz.sln** solution file from **Source\Ex1-UsingEntityFrameworkMigrations\Begin**.</span></span>
2. <span data-ttu-id="9b3b3-176">构建解决方案以便下载并安装**NuGet**程序包依赖项。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-176">Build the solution in order to download and install the **NuGet** package dependencies.</span></span> <span data-ttu-id="9b3b3-177">为此，请右键单击该解决方案，然后单击 "**生成解决方案**" 或按**Ctrl + Shift + B**。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-177">To do this, right-click the solution and click **Build Solution** or press **Ctrl + Shift + B**.</span></span>
3. <span data-ttu-id="9b3b3-178">在 Visual Studio 的 "**工具**" 菜单中，选择 " **NuGet 包管理器**"，然后单击 "**程序包管理器控制台**"。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-178">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
4. <span data-ttu-id="9b3b3-179">在 "**程序包管理器控制台**" 中，输入以下命令，然后按**enter**。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-179">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span> <span data-ttu-id="9b3b3-180">将创建基于现有模型的初始迁移。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-180">An initial migration based on the existing model will be created.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample1.ps1)]

    <span data-ttu-id="9b3b3-181">![启用迁移](maintainable-azure-websites-managing-change-and-scale/_static/image1.png "启用迁移")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-181">![Enabling Migrations](maintainable-azure-websites-managing-change-and-scale/_static/image1.png "Enabling Migrations")</span></span>

    <span data-ttu-id="9b3b3-182">*启用迁移*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-182">*Enabling Migrations*</span></span>

    > [!NOTE]
    > <span data-ttu-id="9b3b3-183">此命令向书呆子阅卷项目添加一个包含名为**Configuration.cs**的文件的**迁移**文件夹。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-183">This command adds a **Migrations** folder to Geek Quiz project that contains a file called **Configuration.cs**.</span></span> <span data-ttu-id="9b3b3-184">**配置**类允许配置迁移对上下文的行为方式。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-184">The **Configuration** class allows you to configure how Migrations behaves for your context.</span></span>
5. <span data-ttu-id="9b3b3-185">启用迁移后，需要更新**配置**类，以便用**书呆子测验**所需的初始数据填充数据库。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-185">With Migrations enabled, you need to update the **Configuration** class to populate the database with the initial data that **Geek Quiz** requires.</span></span> <span data-ttu-id="9b3b3-186">在 "**迁移**" 下，将**Configuration.cs**文件替换为位于此实验室的**Source\Assets**文件夹中的文件。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-186">Under **Migrations**, replace the **Configuration.cs** file with the one located in the **Source\Assets** folder of this lab.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9b3b3-187">因为**迁移**将对每个数据库更新调用**Seed**方法，所以需要确保在数据库中不会复制记录。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-187">Since **Migrations** will call the **Seed** method with every database update, you need to be sure that records are not duplicated in the database.</span></span> <span data-ttu-id="9b3b3-188">**AddOrUpdate**方法有助于防止重复数据。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-188">The **AddOrUpdate** method will help to prevent duplicate data.</span></span>
6. <span data-ttu-id="9b3b3-189">若要添加初始迁移，请输入以下命令，然后按**enter**。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-189">To add an initial migration, enter the following command and then press **Enter**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9b3b3-190">请确保 LocalDB 实例中没有名为 &quot;GeekQuizProd&quot; 的数据库。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-190">Make sure that there is no database named &quot;GeekQuizProd&quot; in your LocalDB instance.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample2.ps1)]

    <span data-ttu-id="9b3b3-191">![添加基础架构迁移](maintainable-azure-websites-managing-change-and-scale/_static/image2.png "添加基础架构迁移")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-191">![Adding base schema migration](maintainable-azure-websites-managing-change-and-scale/_static/image2.png "Adding base schema migration")</span></span>

    <span data-ttu-id="9b3b3-192">*添加基础架构迁移*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-192">*Adding base schema migration*</span></span>

    > [!NOTE]
    > <span data-ttu-id="9b3b3-193">**添加迁移**将基于自上次创建迁移后对模型所做的更改基架下一次迁移。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-193">**Add-Migration** will scaffold the next migration based on changes you have made to your model since the last migration was created.</span></span> <span data-ttu-id="9b3b3-194">在这种情况下，因为它是项目的首次迁移，所以它将添加脚本，以创建在**TriviaContext**类中定义的所有表。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-194">In this case, as it is the first migration of the project, it will add the scripts to create all the tables defined in the **TriviaContext** class.</span></span>
7. <span data-ttu-id="9b3b3-195">通过运行以下命令执行迁移以更新数据库。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-195">Execute the migration to update the database by running the following command.</span></span> <span data-ttu-id="9b3b3-196">对于此命令，您将指定**详细**标志以查看应用于目标数据库的 SQL 语句。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-196">For this command you will specify the **Verbose** flag to view the SQL statements being applied to the target database.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample3.ps1)]

    <span data-ttu-id="9b3b3-197">![正在创建初始数据库](maintainable-azure-websites-managing-change-and-scale/_static/image3.png "正在创建初始数据库")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-197">![Creating initial database](maintainable-azure-websites-managing-change-and-scale/_static/image3.png "Creating initial database")</span></span>

    <span data-ttu-id="9b3b3-198">*正在创建初始数据库*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-198">*Creating initial database*</span></span>

    > [!NOTE]
    > <span data-ttu-id="9b3b3-199">**更新-数据库**将应用任何挂起的到数据库的迁移。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-199">**Update-Database** will apply any pending migrations to the database.</span></span> <span data-ttu-id="9b3b3-200">在这种情况下，它将使用 web.config 文件中定义的连接字符串来创建数据库。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-200">In this case, it will create the database using the connection string defined in your web.config file.</span></span>
8. <span data-ttu-id="9b3b3-201">中转到 "**视图**" 菜单并打开**SQL Server 对象资源管理器**。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-201">Go to **View** menu and open **SQL Server Object Explorer**.</span></span>

    <span data-ttu-id="9b3b3-202">![在 SQL Server 对象资源管理器中打开](maintainable-azure-websites-managing-change-and-scale/_static/image4.png "在 SQL Server 对象资源管理器中打开")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-202">![Open in SQL Server Object Explorer](maintainable-azure-websites-managing-change-and-scale/_static/image4.png "Open in SQL Server Object Explorer")</span></span>

    <span data-ttu-id="9b3b3-203">*在 SQL Server 对象资源管理器中打开*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-203">*Open in SQL Server Object Explorer*</span></span>
9. <span data-ttu-id="9b3b3-204">在 " **SQL Server 对象资源管理器**" 窗口中，右键单击 " **SQL Server** " 节点，然后选择 "**添加 SQL Server ...** " 选项，连接到 LocalDB 实例。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-204">In the **SQL Server Object Explorer** window, connect to your LocalDB instance by right-clicking the **SQL Server** node and selecting **Add SQL Server...** option.</span></span>

    <span data-ttu-id="9b3b3-205">![添加 SQL Server 实例](maintainable-azure-websites-managing-change-and-scale/_static/image5.png "添加 SQL Server 实例")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-205">![Adding a SQL Server Instance](maintainable-azure-websites-managing-change-and-scale/_static/image5.png "Adding a SQL Server Instance")</span></span>

    <span data-ttu-id="9b3b3-206">*将 SQL Server 实例添加到 SQL Server 对象资源管理器*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-206">*Adding a SQL Server instance to SQL Server Object Explorer*</span></span>
10. <span data-ttu-id="9b3b3-207">将**服务器名称**设置为 *（localdb） \v11.0* ，并将**Windows 身份验证**设置为身份验证模式。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-207">Set the **server name** to *(localdb)\v11.0* and leave **Windows Authentication** as your authentication mode.</span></span> <span data-ttu-id="9b3b3-208">单击“ **连接** ”以继续。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-208">Click **Connect** to continue.</span></span>

    <span data-ttu-id="9b3b3-209">![连接到 LocalDB](maintainable-azure-websites-managing-change-and-scale/_static/image6.png "连接到 LocalDB")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-209">![Connecting to LocalDB](maintainable-azure-websites-managing-change-and-scale/_static/image6.png "Connecting to LocalDB")</span></span>

    <span data-ttu-id="9b3b3-210">*连接到 LocalDB*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-210">*Connecting to LocalDB*</span></span>
11. <span data-ttu-id="9b3b3-211">打开**GeekQuizProd**数据库，然后展开 "**表**" 节点。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-211">Open the **GeekQuizProd** database and expand the **Tables** node.</span></span> <span data-ttu-id="9b3b3-212">如您所见，**更新数据库**命令生成了**TriviaContext**类中定义的所有表。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-212">As you can see, the **Update-Database** command generated all the tables defined in the **TriviaContext** class.</span></span> <span data-ttu-id="9b3b3-213">找到**dbo。TriviaQuestions**表并打开 "列" 节点。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-213">Locate the **dbo.TriviaQuestions** table and open the columns node.</span></span> <span data-ttu-id="9b3b3-214">在下一任务中，您将向此表中添加一个新列，并使用**迁移**更新数据库。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-214">In the next task, you will add a new column to this table and update the database using **Migrations**.</span></span>

    <span data-ttu-id="9b3b3-215">![琐碎内容问题列](maintainable-azure-websites-managing-change-and-scale/_static/image7.png "琐碎内容问题列")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-215">![Trivia Questions Columns](maintainable-azure-websites-managing-change-and-scale/_static/image7.png "Trivia Questions Columns")</span></span>

    <span data-ttu-id="9b3b3-216">*琐碎内容问题列*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-216">*Trivia Questions Columns*</span></span>

<a id="Ex1Task2"></a>
#### <a name="task-2--updating-database-schema-using-migrations"></a><span data-ttu-id="9b3b3-217">任务2–使用迁移更新数据库架构</span><span class="sxs-lookup"><span data-stu-id="9b3b3-217">Task 2 – Updating Database Schema Using Migrations</span></span>

<span data-ttu-id="9b3b3-218">在此任务中，您将使用**Entity Framework Code First 迁移**来检测模型的更改，并生成必要的代码来更新数据库。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-218">In this task, you will use **Entity Framework Code First Migrations** to detect a change in your model and generate the necessary code to update the database.</span></span> <span data-ttu-id="9b3b3-219">你将通过向**TriviaQuestions**实体添加新属性来更新该实体。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-219">You will update the **TriviaQuestions** entity by adding a new property to it.</span></span> <span data-ttu-id="9b3b3-220">然后，你将运行命令来创建新的迁移，以将新列包含在表中。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-220">Then you will run commands to create a new Migration to include the new column in the table.</span></span>

1. <span data-ttu-id="9b3b3-221">在**解决方案资源管理器**中，双击位于 "**模型**" 文件夹中的**TriviaQuestion.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-221">In **Solution Explorer**, double-click the **TriviaQuestion.cs** file located inside the **Models** folder.</span></span>
2. <span data-ttu-id="9b3b3-222">添加一个名为 "**提示**" 的新属性，如下面的代码段所示。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-222">Add a new property named **Hint**, as shown in the following code snippet.</span></span>

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample4.cs)]
3. <span data-ttu-id="9b3b3-223">在 "**程序包管理器控制台**" 中，输入以下命令，然后按**enter**。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-223">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span> <span data-ttu-id="9b3b3-224">将创建新的迁移，以反映模型中的更改。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-224">A new migration will be created reflecting the change in our model.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample5.ps1)]

    <span data-ttu-id="9b3b3-225">![添加-迁移](maintainable-azure-websites-managing-change-and-scale/_static/image8.png "Add-Migration")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-225">![Add-Migration](maintainable-azure-websites-managing-change-and-scale/_static/image8.png "Add-Migration")</span></span>

    <span data-ttu-id="9b3b3-226">*添加-迁移*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-226">*Add-Migration*</span></span>

    > [!NOTE]
    > <span data-ttu-id="9b3b3-227">迁移文件由两种方法组成：**向上**和**向下**。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-227">A Migration file is composed of two methods, **Up** and **Down**.</span></span>
    >
    > - <span data-ttu-id="9b3b3-228">**Up**方法用于指定应用程序的当前版本应用程序需要应用于数据库的更改。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-228">The **Up** method will be used to specify what changes the current version of our application need to apply to the database.</span></span>
    > - <span data-ttu-id="9b3b3-229">**Down**用于反转添加到**Up**方法中的更改。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-229">The **Down** is used to reverse the changes we have added to the **Up** method.</span></span>
    >
    > <span data-ttu-id="9b3b3-230">当数据库迁移更新数据库时，它将按时间戳顺序运行所有迁移，并且仅运行自上次更新以来尚未使用的迁移（\_MigrationHistory 表会跟踪已应用的迁移）。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-230">When the Database Migration updates the database, it will run all migrations in the timestamp order, and only those that have not been used since the last update (The \_MigrationHistory table keeps track of which migrations have been applied).</span></span> <span data-ttu-id="9b3b3-231">将调用所有迁移的向上方法，并将所做的更改**设置**为数据库。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-231">The **Up** method of all migrations will be called and will make the changes we have specified to the database.</span></span> <span data-ttu-id="9b3b3-232">如果我们决定返回到以前的迁移，则将调用**Down**方法以按相反顺序重做更改。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-232">If we decide to go back to a previous migration, the **Down** method will be called to redo the changes in a reverse order.</span></span>
4. <span data-ttu-id="9b3b3-233">在 "**程序包管理器控制台**" 中，输入以下命令，然后按**enter**。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-233">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample6.ps1)]
5. <span data-ttu-id="9b3b3-234">TriviaQuestions 命令的输出**生成了** **Alter Table** SQL 语句，以将新列添加到表中，如下图所示。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-234">The output of the **Update-Database** command generated an **Alter Table** SQL statement to add a new column to the **TriviaQuestions** table, as shown in the image below.</span></span>

    <span data-ttu-id="9b3b3-235">![添加了生成列 SQL 语句](maintainable-azure-websites-managing-change-and-scale/_static/image9.png "添加了生成列 SQL 语句")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-235">![Add column SQL statement generated](maintainable-azure-websites-managing-change-and-scale/_static/image9.png "Add column SQL statement generated")</span></span>

    <span data-ttu-id="9b3b3-236">*添加了生成列 SQL 语句*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-236">*Add column SQL statement generated*</span></span>
6. <span data-ttu-id="9b3b3-237">在**SQL Server 对象资源管理器**中，刷新**dbo。TriviaQuestions**表并检查是否显示了新的**提示**列。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-237">In **SQL Server Object Explorer**, refresh the **dbo.TriviaQuestions** table and check that the new **Hint** column is displayed.</span></span>

    <span data-ttu-id="9b3b3-238">![显示新提示列](maintainable-azure-websites-managing-change-and-scale/_static/image10.png "显示新提示列")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-238">![Showing the new Hint Column](maintainable-azure-websites-managing-change-and-scale/_static/image10.png "Showing the new Hint Column")</span></span>

    <span data-ttu-id="9b3b3-239">*显示新提示列*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-239">*Showing the new Hint Column*</span></span>
7. <span data-ttu-id="9b3b3-240">返回到**TriviaQuestion.cs**编辑器，将**StringLength**约束添加到*提示*属性，如下面的代码段所示。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-240">Back in the **TriviaQuestion.cs** editor, add a **StringLength** constraint to the *Hint* property, as shown in the following code snippet.</span></span>

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample7.cs)]
8. <span data-ttu-id="9b3b3-241">在 "**程序包管理器控制台**" 中，输入以下命令，然后按**enter**。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-241">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample8.ps1)]
9. <span data-ttu-id="9b3b3-242">在 "**程序包管理器控制台**" 中，输入以下命令，然后按**enter**。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-242">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample9.ps1)]
10. <span data-ttu-id="9b3b3-243">TriviaQuestions 命令的输出**生成了** **Alter table** SQL 语句以更新表的*提示*列类型，如下图所示。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-243">The output of the **Update-Database** command generated an **Alter Table** SQL statement to update the *hint* column type of the **TriviaQuestions** table, as shown in the image below.</span></span>

    <span data-ttu-id="9b3b3-244">![已生成 Alter column SQL 语句](maintainable-azure-websites-managing-change-and-scale/_static/image11.png "已生成 Alter column SQL 语句")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-244">![Alter column SQL statement generated](maintainable-azure-websites-managing-change-and-scale/_static/image11.png "Alter column SQL statement generated")</span></span>

    <span data-ttu-id="9b3b3-245">*已生成 Alter column SQL 语句*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-245">*Alter column SQL statement generated*</span></span>
11. <span data-ttu-id="9b3b3-246">在**SQL Server 对象资源管理器**中，刷新**dbo。TriviaQuestions**表并检查**提示**列类型是否为**nvarchar （150）** 。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-246">In **SQL Server Object Explorer**, refresh the **dbo.TriviaQuestions** table and check that the **Hint** column type is **nvarchar(150)**.</span></span>

    <span data-ttu-id="9b3b3-247">![显示新约束](maintainable-azure-websites-managing-change-and-scale/_static/image12.png "显示新约束")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-247">![Showing the new constraint](maintainable-azure-websites-managing-change-and-scale/_static/image12.png "Showing the new constraint")</span></span>

    <span data-ttu-id="9b3b3-248">*显示新约束*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-248">*Showing the new constraint*</span></span>

<a id="Exercise2"></a>
### <a name="exercise-2-deploying-a-web-app-to-staging"></a><span data-ttu-id="9b3b3-249">练习2：将 Web 应用部署到过渡环境</span><span class="sxs-lookup"><span data-stu-id="9b3b3-249">Exercise 2: Deploying a Web App to Staging</span></span>

<span data-ttu-id="9b3b3-250">**Azure App Service 中的 Web 应用**可用于执行分阶段发布。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-250">**Web Apps in Azure App Service** enables you to perform staged publishing.</span></span> <span data-ttu-id="9b3b3-251">过渡发布为每个默认生产站点创建一个过渡站点槽，并使你能够在不停机的情况下交换这些槽。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-251">Staged publishing creates a staging site slot for each default production site and enables you to swap these slots with no down time.</span></span> <span data-ttu-id="9b3b3-252">这对于在发布到公共、增量集成站点内容之前验证更改，以及在更改未按预期工作时回滚的操作非常有用。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-252">This is really useful to validate changes before releasing to the public, incrementally integrate site content, and roll back if changes are not working as expected.</span></span>

<span data-ttu-id="9b3b3-253">在此练习中，你将使用 Git 源代码管理将**书呆子测验**应用程序部署到 web 应用的过渡环境。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-253">In this exercise, you will deploy the **Geek Quiz** application to the staging environment of your web app using Git source control.</span></span> <span data-ttu-id="9b3b3-254">为此，需要在管理门户中创建 web 应用并设置所需的组件，配置**Git**存储库，并将应用程序源代码从本地计算机推送到过渡槽。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-254">To do this, you will create the web app and provision the required components at the management portal, configure a **Git** repository and push the application source code from your local computer to the staging slot.</span></span> <span data-ttu-id="9b3b3-255">你还将用在上一个练习中创建的**Code First 迁移**更新生产数据库。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-255">You will also update your production database with the **Code First Migrations** you created in the previous exercise.</span></span> <span data-ttu-id="9b3b3-256">然后，你将在此测试环境中执行应用程序以验证其操作。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-256">You will then execute the application in this test environment to verify its operation.</span></span> <span data-ttu-id="9b3b3-257">一旦您认为它是根据您的预期工作，您就会将该应用程序提升到生产环境。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-257">Once you are satisfied that it is working according to your expectations, you will promote the application to production.</span></span>

> [!NOTE]
> <span data-ttu-id="9b3b3-258">若要启用过渡发布，web 应用必须处于 "**标准" 模式**。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-258">To enable staged publishing, the web app must be in **Standard mode**.</span></span> <span data-ttu-id="9b3b3-259">请注意，如果你将 web 应用更改为 "标准" 模式，则会产生额外费用。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-259">Note that additional charges will be incurred if you change your web app to Standard mode.</span></span> <span data-ttu-id="9b3b3-260">有关定价的详细信息，请参阅[应用服务定价](https://azure.microsoft.com/pricing/details/app-service/)。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-260">For more information about pricing, see [App Service Pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

<a id="Ex2Task1"></a>
#### <a name="task-1--creating-a-web-app-in-azure-app-service"></a><span data-ttu-id="9b3b3-261">任务1–在 Azure App Service 中创建 Web 应用</span><span class="sxs-lookup"><span data-stu-id="9b3b3-261">Task 1 – Creating a Web App in Azure App Service</span></span>

<span data-ttu-id="9b3b3-262">在此任务中，你将在管理门户的**Azure App Service**中创建 web 应用。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-262">In this task, you will create a web app in **Azure App Service** from the management portal.</span></span> <span data-ttu-id="9b3b3-263">你还将配置一个**SQL 数据库**来持久保存应用程序数据，并为源代码管理配置一个本地 Git 存储库。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-263">You will also configure a **SQL Database** to persist the application data, and configure a local Git repository for source control.</span></span>

1. <span data-ttu-id="9b3b3-264">请参阅[Azure 管理门户](https://manage.windowsazure.com)，并使用与你的订阅关联的 Microsoft 帐户登录。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-264">Go to the [Azure management portal](https://manage.windowsazure.com) and sign in using the Microsoft account associated with your subscription.</span></span>

    ![登录到 Azure 管理门户](maintainable-azure-websites-managing-change-and-scale/_static/image13.png)

    <span data-ttu-id="9b3b3-266">*登录到 Azure 管理门户*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-266">*Sign in to the Azure management portal*</span></span>
2. <span data-ttu-id="9b3b3-267">单击页面底部命令栏中的 "**新建**"。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-267">Click **New** in the command bar at the bottom of the page.</span></span>

    <span data-ttu-id="9b3b3-268">![创建新的 web 应用](maintainable-azure-websites-managing-change-and-scale/_static/image14.png "创建新的 web 应用")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-268">![Creating a new web app](maintainable-azure-websites-managing-change-and-scale/_static/image14.png "Creating a new web app")</span></span>

    <span data-ttu-id="9b3b3-269">*创建新的 web 应用*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-269">*Creating a new web app*</span></span>
3. <span data-ttu-id="9b3b3-270">单击 "**计算**"、"**网站**"，然后单击 "**自定义创建**"。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-270">Click **Compute**, **Website** and then **Custom Create**.</span></span>

    <span data-ttu-id="9b3b3-271">![使用 "自定义创建" 创建新的 web 应用](maintainable-azure-websites-managing-change-and-scale/_static/image15.png "使用 "自定义创建" 创建新的 web 应用")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-271">![Creating a new web app using Custom Create](maintainable-azure-websites-managing-change-and-scale/_static/image15.png "Creating a new web app using Custom Create")</span></span>

    <span data-ttu-id="9b3b3-272">*使用 "自定义创建" 创建新的 web 应用*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-272">*Creating a new web app using Custom Create*</span></span>
4. <span data-ttu-id="9b3b3-273">在 "**新建网站-自定义创建**" 对话框中，提供可用的**URL** （例如*书呆子*），在 "**区域**" 下拉列表中选择一个位置，然后在 "**数据库**" 下拉列表中选择 "**创建新的 SQL 数据库**"。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-273">In the **New Website - Custom Create** dialog box, provide an available **URL** (e.g. *geek-quiz*), select a location in the **Region** drop-down list, and select **Create a new SQL database** in the **Database** drop-down list.</span></span> <span data-ttu-id="9b3b3-274">最后，选中 "**从源代码管理发布**" 复选框，然后单击 "**下一步**"。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-274">Finally, select the **Publish from source control** check box and click **Next**.</span></span>

    ![自定义新的 web 应用](maintainable-azure-websites-managing-change-and-scale/_static/image16.png)

    <span data-ttu-id="9b3b3-276">*自定义新的 web 应用*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-276">*Customizing the new web app*</span></span>
5. <span data-ttu-id="9b3b3-277">指定数据库设置的下列信息：</span><span class="sxs-lookup"><span data-stu-id="9b3b3-277">Specify the following information for the database settings:</span></span>

   - <span data-ttu-id="9b3b3-278">在 "**名称**" 文本框中，输入数据库名称（例如， *geekquiz\_db*）</span><span class="sxs-lookup"><span data-stu-id="9b3b3-278">In the **Name** text box, enter a database name (e.g. *geekquiz\_db*)</span></span>
   - <span data-ttu-id="9b3b3-279">在 "服务器"**下拉**列表中，选择 "**新建 SQL 数据库服务器**"。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-279">In the Server **drop-down** list, select **New SQL database server**.</span></span> <span data-ttu-id="9b3b3-280">或者，您可以选择现有服务器。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-280">Alternatively, you can select an existing server.</span></span>
   - <span data-ttu-id="9b3b3-281">在 "**数据库用户名**" 和 "**数据库密码**" 框中，输入 SQL 数据库服务器的管理员用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-281">In the **Database username** and **Database password** boxes, enter the administrator username and password for the SQL database server.</span></span> <span data-ttu-id="9b3b3-282">如果选择一个已创建的服务器，系统会提示输入密码。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-282">If you select a server you have already created, you will be prompted for the password.</span></span>

     ![指定数据库设置](maintainable-azure-websites-managing-change-and-scale/_static/image17.png)

     <span data-ttu-id="9b3b3-284">*指定数据库设置*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-284">*Specifying the database settings*</span></span>
6. <span data-ttu-id="9b3b3-285">单击 **“下一步”** 以继续。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-285">Click **Next** to continue.</span></span>
7. <span data-ttu-id="9b3b3-286">选择要使用的源代码管理的 "**本地 Git 存储库**"，然后单击 "**下一步**"。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-286">Select **Local Git repository** for the source control to use and click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9b3b3-287">系统可能会提示你输入部署凭据（用户名和密码）。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-287">You may be prompted for the deployment credentials (a username and password).</span></span>

    ![创建 Git 存储库](maintainable-azure-websites-managing-change-and-scale/_static/image18.png)

    <span data-ttu-id="9b3b3-289">*创建 Git 存储库*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-289">*Creating the Git repository*</span></span>
8. <span data-ttu-id="9b3b3-290">等待，直到创建新的 web 应用。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-290">Wait until the new web app is created.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9b3b3-291">默认情况下，Azure 在*azurewebsites.net*提供域，还可以使用 azure 管理门户设置自定义域。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-291">By default, Azure provides domains at *azurewebsites.net* but also gives you the possibility to set custom domains using the Azure management portal.</span></span> <span data-ttu-id="9b3b3-292">但是，如果你使用某些 Azure App Service 模式，则只能管理自定义域。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-292">However, you can only manage custom domains if you are using certain Azure App Service modes.</span></span>
    >
    > <span data-ttu-id="9b3b3-293">Azure App Service 提供免费、共享、基本、标准和高级版。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-293">Azure App Service is available in Free, Shared, Basic, Standard, and Premium editions.</span></span> <span data-ttu-id="9b3b3-294">在 "免费" 和 "共享" 模式下，所有 web 应用都在多租户环境中运行，并具有 CPU、内存和网络使用情况的配额。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-294">In Free and Shared mode, all web apps run in a multi-tenant environment and have quotas for CPU, Memory, and Network usage.</span></span> <span data-ttu-id="9b3b3-295">最大可用应用数可能因计划而异。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-295">The maximum number of free apps may vary with your plan.</span></span> <span data-ttu-id="9b3b3-296">在 "标准" 模式下，你可以选择在与标准 Azure 计算资源相对应的专用虚拟机上运行的应用。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-296">In Standard mode, you choose which apps run on dedicated virtual machines that correspond to the standard Azure compute resources.</span></span> <span data-ttu-id="9b3b3-297">可在 web 应用的 "**缩放**" 菜单中找到 web 应用模式配置。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-297">You can find the web app mode configuration in the **Scale** menu of your web app.</span></span>
    >
    > <span data-ttu-id="9b3b3-298">![Azure App Service 模式](maintainable-azure-websites-managing-change-and-scale/_static/image19.png "Azure App Service 模式")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-298">![Azure App Service Modes](maintainable-azure-websites-managing-change-and-scale/_static/image19.png "Azure App Service Modes")</span></span>
    >
    > <span data-ttu-id="9b3b3-299">如果你使用的是 "**共享**" 或 "**标准**" 模式，你将能够通过转到应用的 "**配置**" 菜单，并在 "*域名*" 下单击 "**管理域**" 来管理 web 应用的自定义域。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-299">If you are using **Shared** or **Standard** mode, you will be able to manage custom domains for your web app by going to your app's **Configure** menu and clicking **Manage Domains** under *domain names*.</span></span>
    >
    > <span data-ttu-id="9b3b3-300">![管理域](maintainable-azure-websites-managing-change-and-scale/_static/image20.png "管理域")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-300">![Manage Domains](maintainable-azure-websites-managing-change-and-scale/_static/image20.png "Manage Domains")</span></span>
    >
    > <span data-ttu-id="9b3b3-301">![管理自定义域](maintainable-azure-websites-managing-change-and-scale/_static/image21.png "管理自定义域")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-301">![Manage Custom Domains](maintainable-azure-websites-managing-change-and-scale/_static/image21.png "Manage Custom Domains")</span></span>
9. <span data-ttu-id="9b3b3-302">创建 web 应用后，单击 " **URL** " 列下的链接，检查新的 web 应用是否正在运行。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-302">Once the web app is created, click the link under the **URL** column to check that the new web app is running.</span></span>

    ![浏览到新的 web 应用](maintainable-azure-websites-managing-change-and-scale/_static/image22.png)

    <span data-ttu-id="9b3b3-304">*浏览到新的 web 应用*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-304">*Browsing to the new web app*</span></span>

    ![web 应用正在运行](maintainable-azure-websites-managing-change-and-scale/_static/image23.png)

    <span data-ttu-id="9b3b3-306">*web 应用正在运行*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-306">*web app running*</span></span>

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-the-production-sql-database"></a><span data-ttu-id="9b3b3-307">任务2–创建生产 SQL 数据库</span><span class="sxs-lookup"><span data-stu-id="9b3b3-307">Task 2 – Creating the Production SQL Database</span></span>

<span data-ttu-id="9b3b3-308">在此任务中，你将使用**Entity Framework Code First 迁移**创建面向你在上一任务中创建的**Azure SQL 数据库**实例的数据库。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-308">In this task, you will use the **Entity Framework Code First Migrations** to create the database targeting the **Azure SQL Database** instance you created in the previous task.</span></span>

1. <span data-ttu-id="9b3b3-309">在管理门户中，导航到在上一任务中创建的 web 应用，并转到其**仪表板**。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-309">In the Management Portal, navigate to the web app you created in the previous task and go to its **Dashboard**.</span></span>
2. <span data-ttu-id="9b3b3-310">在 "**仪表板**" 页上，单击 **"速览" 部分下**的 "**查看连接字符串**" 链接。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-310">In the **Dashboard** page, click **View connection strings** link under the **quick glance** section.</span></span>

    <span data-ttu-id="9b3b3-311">![查看连接字符串](maintainable-azure-websites-managing-change-and-scale/_static/image24.png "查看连接字符串")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-311">![View connection strings](maintainable-azure-websites-managing-change-and-scale/_static/image24.png "View connection strings")</span></span>

    <span data-ttu-id="9b3b3-312">*查看连接字符串*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-312">*View connection strings*</span></span>
3. <span data-ttu-id="9b3b3-313">复制 "**连接字符串**" 值并关闭对话框。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-313">Copy the **connection string** value and close the dialog box.</span></span>

    <span data-ttu-id="9b3b3-314">![Azure 管理门户中的连接字符串](maintainable-azure-websites-managing-change-and-scale/_static/image25.png "Azure 管理门户中的连接字符串")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-314">![Connection String in Azure Management Portal](maintainable-azure-websites-managing-change-and-scale/_static/image25.png "Connection String in Azure Management Portal")</span></span>

    <span data-ttu-id="9b3b3-315">*Azure 管理门户中的连接字符串*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-315">*Connection String in Azure Management Portal*</span></span>
4. <span data-ttu-id="9b3b3-316">单击 " **Sql 数据库**" 以查看 Azure 中的 sql 数据库列表</span><span class="sxs-lookup"><span data-stu-id="9b3b3-316">Click **SQL Databases** to see the list of SQL databases in Azure</span></span>

    <span data-ttu-id="9b3b3-317">![SQL 数据库菜单](maintainable-azure-websites-managing-change-and-scale/_static/image26.png "SQL 数据库菜单")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-317">![SQL Database menu](maintainable-azure-websites-managing-change-and-scale/_static/image26.png "SQL Database menu")</span></span>

    <span data-ttu-id="9b3b3-318">*SQL 数据库菜单*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-318">*SQL Database menu*</span></span>
5. <span data-ttu-id="9b3b3-319">找到在上一任务中创建的数据库，然后单击该服务器。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-319">Locate the database you created in the previous task and click on the Server.</span></span>

    <span data-ttu-id="9b3b3-320">![SQL 数据库服务器](maintainable-azure-websites-managing-change-and-scale/_static/image27.png "SQL 数据库服务器")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-320">![SQL Database server](maintainable-azure-websites-managing-change-and-scale/_static/image27.png "SQL Database server")</span></span>

    <span data-ttu-id="9b3b3-321">*SQL 数据库服务器*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-321">*SQL Database server*</span></span>
6. <span data-ttu-id="9b3b3-322">在服务器的 "**快速入门**" 页上，单击 "**配置**"。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-322">In the **Quick Start** page of the server, click on **Configure**.</span></span>

    <span data-ttu-id="9b3b3-323">![配置菜单](maintainable-azure-websites-managing-change-and-scale/_static/image28.png "配置菜单")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-323">![Configure menu](maintainable-azure-websites-managing-change-and-scale/_static/image28.png "Configure menu")</span></span>

    <span data-ttu-id="9b3b3-324">*配置菜单*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-324">*Configure menu*</span></span>
7. <span data-ttu-id="9b3b3-325">在 "**允许的 ip 地址**" 部分中，单击 **"添加到允许的 ip 地址"** 链接，以使你的 IP 能够连接到 SQL 数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-325">In the **Allowed IP addresses** section, click on **Add to the allowed IP addresses** link to enable your IP to connect to the SQL Database server.</span></span>

    <span data-ttu-id="9b3b3-326">![允许的 IP 地址](maintainable-azure-websites-managing-change-and-scale/_static/image29.png "允许的 IP 地址")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-326">![Allowed IP addresses](maintainable-azure-websites-managing-change-and-scale/_static/image29.png "Allowed IP addresses")</span></span>

    <span data-ttu-id="9b3b3-327">*允许的 IP 地址*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-327">*Allowed IP addresses*</span></span>
8. <span data-ttu-id="9b3b3-328">单击页面底部的 "**保存**" 以完成该步骤。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-328">Click **Save** at the bottom of the page to complete the step.</span></span>
9. <span data-ttu-id="9b3b3-329">切换回 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-329">Switch back to Visual Studio.</span></span>
10. <span data-ttu-id="9b3b3-330">在**包管理器控制台**中，执行以下命令，将 *[你的连接字符串]* 占位符替换为从 Azure 复制的连接字符串</span><span class="sxs-lookup"><span data-stu-id="9b3b3-330">In the **Package Manager Console**, execute the following command replacing *[YOUR-CONNECTION-STRING]* placeholder with the connection string you copied from Azure</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample10.ps1)]

    <span data-ttu-id="9b3b3-331">![更新面向 Windows Azure SQL 数据库的数据库](maintainable-azure-websites-managing-change-and-scale/_static/image30.png "更新面向 Windows Azure SQL 数据库的数据库")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-331">![Update database targeting Windows Azure SQL Database](maintainable-azure-websites-managing-change-and-scale/_static/image30.png "Update database targeting Windows Azure SQL Database")</span></span>

    <span data-ttu-id="9b3b3-332">*更新面向 Azure SQL 数据库的数据库*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-332">*Update database targeting Azure SQL Database*</span></span>

<a id="Ex2Task3"></a>
#### <a name="task-3--deploying-geek-quiz-to-staging-using-git"></a><span data-ttu-id="9b3b3-333">任务3–使用 Git 将书呆子测验部署到过渡</span><span class="sxs-lookup"><span data-stu-id="9b3b3-333">Task 3 – Deploying Geek Quiz to Staging Using Git</span></span>

<span data-ttu-id="9b3b3-334">在此任务中，将在 web 应用中启用过渡发布。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-334">In this task, you will enable staged publishing in your web app.</span></span> <span data-ttu-id="9b3b3-335">然后，将使用 Git 将书呆子测验应用程序从本地计算机直接发布到 web 应用的过渡环境。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-335">Then, you will use Git to publish the Geek Quiz application directly from your local computer to the staging environment of your web app.</span></span>

1. <span data-ttu-id="9b3b3-336">返回到门户，并在 "**名称**" 列下单击 web 应用的名称以显示管理页面。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-336">Go back to the portal and click the name of the web app under the **Name** column to display the management pages.</span></span>

    ![打开 web 应用管理页](maintainable-azure-websites-managing-change-and-scale/_static/image31.png)

    <span data-ttu-id="9b3b3-338">*打开 web 应用管理页*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-338">*Opening the web app management pages*</span></span>
2. <span data-ttu-id="9b3b3-339">导航到 "**缩放**" 页。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-339">Navigate to the **Scale** page.</span></span> <span data-ttu-id="9b3b3-340">在 "**常规**" 部分下，选择 "**标准**" 作为配置，并单击命令栏中的 "**保存**"。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-340">Under the **general** section, select **Standard** for the configuration and click **Save** in the command bar.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9b3b3-341">若要在 "**标准**" 模式下运行当前区域和订阅中的所有 web 应用，请将 "选择**站点**" 配置中的 "**全**选" 复选框保持选中状态。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-341">To run all web apps in the current region and subscription in **Standard** mode, leave the **Select All** check box selected in the **Choose Sites** configuration.</span></span> <span data-ttu-id="9b3b3-342">否则，请清除 "**全选**" 复选框。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-342">Otherwise, clear the **Select All** check box.</span></span>

    <span data-ttu-id="9b3b3-343">![将 web 应用升级到标准模式](maintainable-azure-websites-managing-change-and-scale/_static/image32.png "将 web 应用升级到标准模式")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-343">![Upgrading the web app to Standard mode](maintainable-azure-websites-managing-change-and-scale/_static/image32.png "Upgrading the web app to Standard mode")</span></span>

    <span data-ttu-id="9b3b3-344">*将 Web 应用升级到标准模式*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-344">*Upgrading the Web App to Standard mode*</span></span>
3. <span data-ttu-id="9b3b3-345">单击 **"是"** 确认更改。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-345">Click **Yes** to confirm the changes.</span></span>

    <span data-ttu-id="9b3b3-346">![确认更改为 "标准" 模式](maintainable-azure-websites-managing-change-and-scale/_static/image33.png "继续更改 web 应用模式")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-346">![Confirming the change to Standard mode](maintainable-azure-websites-managing-change-and-scale/_static/image33.png "Continuing with the changing of the web app mode")</span></span>

    <span data-ttu-id="9b3b3-347">*确认更改为 "标准" 模式*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-347">*Confirming the change to Standard mode*</span></span>
4. <span data-ttu-id="9b3b3-348">中转到 "**仪表板**" 页，然后单击 "**速览**" 部分下的 "**启用过渡发布**"。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-348">Go to the **Dashboard** page and click **Enable staged publishing** under the **quick glance** section.</span></span>

    <span data-ttu-id="9b3b3-349">![启用过渡发布](maintainable-azure-websites-managing-change-and-scale/_static/image34.png "启用过渡发布")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-349">![Enabling staged publishing](maintainable-azure-websites-managing-change-and-scale/_static/image34.png "Enabling staged publishing")</span></span>

    <span data-ttu-id="9b3b3-350">*启用过渡发布*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-350">*Enabling staged publishing*</span></span>
5. <span data-ttu-id="9b3b3-351">单击 **"是"** 以启用过渡发布。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-351">Click **Yes** to enable staged publishing.</span></span>

    <span data-ttu-id="9b3b3-352">![正在确认暂存发布](maintainable-azure-websites-managing-change-and-scale/_static/image35.png "单击 "是" 以启用过渡发布")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-352">![Confirming staged publishing](maintainable-azure-websites-managing-change-and-scale/_static/image35.png "Clicking Yes to enable staged publishing")</span></span>

    <span data-ttu-id="9b3b3-353">*正在确认暂存发布*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-353">*Confirming staged publishing*</span></span>
6. <span data-ttu-id="9b3b3-354">在 web 应用列表中，展开 web 应用名称左侧的标记以显示过渡站点槽。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-354">In the list of web apps, expand the mark to the left of your web app name to display the staging site slot.</span></span> <span data-ttu-id="9b3b3-355">它包含你的 web 应用的名称，后跟 " ***（过渡）***"。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-355">It has the name of your web app followed by ***(staging)***.</span></span> <span data-ttu-id="9b3b3-356">单击暂存站点以切换到 "管理" 页。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-356">Click the staging site to go to the management page.</span></span>

    <span data-ttu-id="9b3b3-357">![导航到过渡 web 应用](maintainable-azure-websites-managing-change-and-scale/_static/image36.png "导航到过渡 web 应用")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-357">![Navigating to the staging web app](maintainable-azure-websites-managing-change-and-scale/_static/image36.png "Navigating to the staging web app")</span></span>

    <span data-ttu-id="9b3b3-358">*导航到过渡应用*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-358">*Navigating to the staging app*</span></span>
7. <span data-ttu-id="9b3b3-359">请注意，此管理页看起来与任何其他 web 应用程序的管理页一样。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-359">Notice that he management page looks like any other web app's management page.</span></span> <span data-ttu-id="9b3b3-360">导航到 "**部署**" 页并复制 " **Git URL** " 值。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-360">Navigate to the **Deployments** page and copy the **Git URL** value.</span></span> <span data-ttu-id="9b3b3-361">稍后在本练习中将使用它。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-361">You will use it later in this exercise.</span></span>

    ![复制 Git URL 值](maintainable-azure-websites-managing-change-and-scale/_static/image37.png)

    <span data-ttu-id="9b3b3-363">*复制 Git URL 值*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-363">*Copying the Git URL value*</span></span>
8. <span data-ttu-id="9b3b3-364">打开新的**Git Bash**控制台并执行以下命令。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-364">Open a new **Git Bash** console and execute the following commands.</span></span> <span data-ttu-id="9b3b3-365">将 *[应用程序路径]* 占位符更新为**GeekQuiz**解决方案的路径，该路径位于此实验室的**Source\Ex1-DeployingWebSiteToStaging\Begin**文件夹中。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-365">Update the *[YOUR-APPLICATION-PATH]* placeholder with the path to the **GeekQuiz** solution, located in the **Source\Ex1-DeployingWebSiteToStaging\Begin** folder of this lab.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample11.cmd)]

    ![Git 初始化和首次提交](maintainable-azure-websites-managing-change-and-scale/_static/image38.png)

    <span data-ttu-id="9b3b3-367">*Git 初始化和首次提交*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-367">*Git initialization and first commit*</span></span>
9. <span data-ttu-id="9b3b3-368">运行以下命令，将 web 应用推送到远程**Git**存储库。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-368">Run the following command to push your web app to the remote **Git** repository.</span></span> <span data-ttu-id="9b3b3-369">将占位符替换为你从管理门户获取的 URL。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-369">Replace the placeholder with the URL you obtained from the management portal.</span></span> <span data-ttu-id="9b3b3-370">系统将提示你输入部署密码。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-370">You will be prompted for your deployment password.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample12.cmd)]

    ![推送到 Microsoft Azure](maintainable-azure-websites-managing-change-and-scale/_static/image39.png)

    <span data-ttu-id="9b3b3-372">*推送到 Azure*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-372">*Pushing to Azure*</span></span>

    > [!NOTE]
    > <span data-ttu-id="9b3b3-373">将内容部署到 web 应用的 FTP 主机或 GIT 存储库时，必须使用从 web 应用的**快速入门**或**仪表板**管理页创建的**部署凭据**进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-373">When you deploy content to the FTP host or GIT repository of a web app, you must authenticate using the **deployment credentials** that you created from the web app's **Quick Start** or **Dashboard** management pages.</span></span> <span data-ttu-id="9b3b3-374">如果你不知道你的部署凭据，则可以使用管理门户轻松地重置它们。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-374">If you do not know your deployment credentials you can easily reset them using the management portal.</span></span> <span data-ttu-id="9b3b3-375">打开 web 应用的 "**仪表板**" 页，然后单击 "**重置部署凭据**" 链接。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-375">Open the web app **Dashboard** page and click the **Reset your deployment credentials** link.</span></span> <span data-ttu-id="9b3b3-376">提供新密码，并单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-376">Provide a new password and click **OK**.</span></span> <span data-ttu-id="9b3b3-377">部署凭据可用于与你的订阅关联的所有 web 应用。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-377">Deployment credentials are valid for use with all web apps associated with your subscription.</span></span>
10. <span data-ttu-id="9b3b3-378">若要验证是否已成功将 web 应用推送到 Azure，请返回到管理门户，然后单击 "**网站**"。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-378">In order to verify the web app was successfully pushed to Azure, go back to the management portal and click **Websites**.</span></span>
11. <span data-ttu-id="9b3b3-379">找到 web 应用，然后展开该条目以显示过渡站点槽。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-379">Locate your web app and expand the entry to display the staging site slot.</span></span> <span data-ttu-id="9b3b3-380">单击其**名称**以打开 "管理" 页。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-380">Click its **Name** to go to the management page.</span></span>
12. <span data-ttu-id="9b3b3-381">单击 "**部署**" 以查看**部署历史记录**。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-381">Click **Deployments** to see the **deployment history**.</span></span> <span data-ttu-id="9b3b3-382">使用 *&quot;初始提交&quot;* 验证是否存在**活动的部署**。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-382">Verify that there is an **Active Deployment** with your *&quot;Initial Commit&quot;*.</span></span>

    ![活动部署](maintainable-azure-websites-managing-change-and-scale/_static/image40.png)

    <span data-ttu-id="9b3b3-384">*活动部署*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-384">*Active deployment*</span></span>
13. <span data-ttu-id="9b3b3-385">最后，单击命令栏中的 "**浏览**"，转到 web 应用。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-385">Finally, click **Browse** in the command bar to go to the web app.</span></span>

    ![浏览 web 应用](maintainable-azure-websites-managing-change-and-scale/_static/image41.png)

    <span data-ttu-id="9b3b3-387">*浏览 web 应用*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-387">*Browse web app*</span></span>
14. <span data-ttu-id="9b3b3-388">如果已成功部署应用程序，你将看到书呆子测验登录页。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-388">If the application is successfully deployed, you will see the Geek Quiz login page.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9b3b3-389">部署的应用程序的地址 URL 包含你的 web 应用的名称，并在*中间进行过渡*。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-389">The address URL of the deployed application contains the name of your web app followed by *-staging*.</span></span>

    ![在过渡环境中运行的应用程序](maintainable-azure-websites-managing-change-and-scale/_static/image42.png)

    <span data-ttu-id="9b3b3-391">*在过渡环境中运行的应用程序*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-391">*Application running in the staging environment*</span></span>
15. <span data-ttu-id="9b3b3-392">如果要浏览应用程序，请单击 "**注册**" 以注册新用户。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-392">If you wish to explore the application, click **Register** to register a new user.</span></span> <span data-ttu-id="9b3b3-393">输入用户名、电子邮件地址和密码来填写帐户详细信息。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-393">Complete the account details by entering a user name, email address and password.</span></span> <span data-ttu-id="9b3b3-394">接下来，应用程序会显示测验的第一个问题。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-394">Next, the application shows the first question of the quiz.</span></span> <span data-ttu-id="9b3b3-395">回答几个问题，以确保它按预期方式工作。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-395">Answer a few questions to make sure it is working as expected.</span></span>

    ![可供使用的应用程序](maintainable-azure-websites-managing-change-and-scale/_static/image43.png)

    <span data-ttu-id="9b3b3-397">*可供使用的应用程序*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-397">*Application ready to be used*</span></span>

<a id="Ex2Task4"></a>
#### <a name="task-4--promoting-the-web-app-to-production"></a><span data-ttu-id="9b3b3-398">任务 4-将 Web 应用升级到生产环境</span><span class="sxs-lookup"><span data-stu-id="9b3b3-398">Task 4 – Promoting the Web App to Production</span></span>

<span data-ttu-id="9b3b3-399">在过渡环境中验证 web 应用是否正常工作后，就可以将其升级到生产环境了。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-399">Now that you have verified that the web app is working correctly in the staging environment, you are ready to promote it to production.</span></span> <span data-ttu-id="9b3b3-400">在此任务中，你要将过渡站点槽与生产站点槽交换。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-400">In this task, you will swap the staging site slot with the production site slot.</span></span>

1. <span data-ttu-id="9b3b3-401">返回到管理门户，并选择 "暂存" 站点槽。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-401">Go back to the management portal and select the staging site slot.</span></span> <span data-ttu-id="9b3b3-402">在命令栏中单击 "**交换**"。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-402">Click **Swap** in the command bar.</span></span>

    ![交换到生产](maintainable-azure-websites-managing-change-and-scale/_static/image44.png)

    <span data-ttu-id="9b3b3-404">*交换到生产*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-404">*Swap to production*</span></span>
2. <span data-ttu-id="9b3b3-405">在确认对话框中单击 **"是"** 以继续执行交换操作。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-405">Click **Yes** in the confirmation dialog box to proceed with the swap operation.</span></span> <span data-ttu-id="9b3b3-406">Azure 会立即将生产站点的内容与过渡站点的内容交换。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-406">Azure will immediately swap the content of the production site with the content of the staging site.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9b3b3-407">过渡版版本中的某些设置将自动复制到生产版本（例如，连接字符串替代、处理程序映射等），但其他设置将不会更改（例如 DNS 终结点、SSL 绑定等）。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-407">Some settings from the staged version will automatically be copied to the production version (e.g. connection string overrides, handler mappings, etc.) but other settings will not change (e.g. DNS endpoints, SSL bindings, etc.).</span></span>

    ![正在确认交换操作](maintainable-azure-websites-managing-change-and-scale/_static/image45.png)

    <span data-ttu-id="9b3b3-409">*正在确认交换操作*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-409">*Confirming swap operation*</span></span>
3. <span data-ttu-id="9b3b3-410">交换完成后，选择 "生产" 槽，并单击命令栏中的 "**浏览**" 以打开生产站点。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-410">Once the swap is complete, select the production slot and click **Browse** in the command bar to open the production site.</span></span> <span data-ttu-id="9b3b3-411">请注意地址栏中的 URL。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-411">Notice the URL in the address bar.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9b3b3-412">可能需要刷新浏览器以清除缓存。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-412">You might need to refresh your browser to clear cache.</span></span> <span data-ttu-id="9b3b3-413">在 Internet Explorer 中，可以通过按**CTRL + R**来完成此操作。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-413">In Internet Explorer, you can do this by pressing **CTRL+R**.</span></span>

    ![在生产环境中运行的 Web 应用](maintainable-azure-websites-managing-change-and-scale/_static/image46.png)
4. <span data-ttu-id="9b3b3-415">在**GitBash**控制台中，更新本地 Git 存储库的远程 URL，使其面向生产槽。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-415">In the **GitBash** console, update the remote URL for the local Git repository to target the production slot.</span></span> <span data-ttu-id="9b3b3-416">为此，请运行以下命令，将占位符替换为部署用户名和 web 应用名称。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-416">To do this, run the following command replacing the placeholders with your deployment username and the name of your web app.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9b3b3-417">在以下练习中，你会将更改推送到生产站点，而不是仅针对实验室的简单性进行过渡。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-417">In the following exercises, you will push changes to the production site instead of staging just for the simplicity of the lab.</span></span> <span data-ttu-id="9b3b3-418">在实际方案中，建议在升级到生产环境之前，验证过渡环境中的更改。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-418">In a real-world scenario, it is recommended to verify the changes in the staging environment before promoting to production.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample13.cmd)]

<a id="Exercise3"></a>
### <a name="exercise-3-performing-deployment-rollback-in-production"></a><span data-ttu-id="9b3b3-419">练习3：在生产环境中执行部署回滚</span><span class="sxs-lookup"><span data-stu-id="9b3b3-419">Exercise 3: Performing Deployment Rollback in Production</span></span>

<span data-ttu-id="9b3b3-420">在某些情况下，如果你使用的是 "**免费**" 或 "**共享**" 模式，则无需使用过渡槽在过渡与生产之间执行热交换。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-420">There are scenarios where you do not have a staging slot to perform hot swap between staging and production, for example, if you are working with **Free** or **Shared** mode.</span></span> <span data-ttu-id="9b3b3-421">在这些情况下，在部署到生产环境之前，你应该在测试环境中测试你的应用程序（本地或远程站点）。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-421">In those scenarios, you should test your application in a testing environment –either locally or in a remote site– before deploying to production.</span></span> <span data-ttu-id="9b3b3-422">但是，在测试阶段未检测到的问题可能出现在生产站点中。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-422">However, it is possible that an issue not detected during the testing phase may arise in the production site.</span></span> <span data-ttu-id="9b3b3-423">在这种情况下，一定要使用一种机制，尽快尽快切换到以前的、更稳定的应用程序版本。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-423">In this case, it is important to have a mechanism to easily switch to a previous and more stable version of the application as quickly as possible.</span></span>

<span data-ttu-id="9b3b3-424">在**Azure App Service**中，通过源代码管理进行持续部署可让你使用管理门户中的 "重新**部署**" 操作。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-424">In **Azure App Service**, continuous deployment from source control makes this possible thanks to the **redeploy** action available in the management portal.</span></span> <span data-ttu-id="9b3b3-425">Azure 会跟踪与推送到存储库的提交相关联的部署，并提供一个选项，用于随时使用你以前的任何部署重新部署应用程序。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-425">Azure keeps track of the deployments associated with the commits pushed to the repository and provides an option to redeploy your application using any of your previous deployments, at any time.</span></span>

<span data-ttu-id="9b3b3-426">在本练习中，您将在**书呆子测验**应用程序中对代码进行更改，以故意注入*bug*。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-426">In this exercise you will perform a change to the code in the **Geek Quiz** application that intentionally injects a *bug*.</span></span> <span data-ttu-id="9b3b3-427">你要将应用程序部署到生产环境以查看错误，然后你将利用重新部署功能返回到以前的状态。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-427">You will deploy the application to production to see the error, and then you will take advantage of the redeploy feature to go back to the previous state.</span></span>

<a id="Ex3Task1"></a>
#### <a name="task-1--updating-the-geek-quiz-application"></a><span data-ttu-id="9b3b3-428">任务1–更新书呆子测验应用程序</span><span class="sxs-lookup"><span data-stu-id="9b3b3-428">Task 1 – Updating the Geek Quiz Application</span></span>

<span data-ttu-id="9b3b3-429">在此任务中，您将重构**TriviaController**类的一小段代码，以便将从数据库中检索所选测验选项的部分逻辑提取到新方法中。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-429">In this task, you will refactor a small piece of code of the **TriviaController** class to extract part of the logic that retrieves the selected quiz option from the database into a new method.</span></span>

1. <span data-ttu-id="9b3b3-430">切换到 Visual Studio 实例，其中包含上一练习中的**GeekQuiz**解决方案。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-430">Switch to the Visual Studio instance with the **GeekQuiz** solution from the previous exercise.</span></span>
2. <span data-ttu-id="9b3b3-431">在**解决方案资源管理器**中，打开 "**控制器**" 文件夹中的**TriviaController.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-431">In **Solution Explorer**, open the **TriviaController.cs** file inside the **Controllers** folder.</span></span>
3. <span data-ttu-id="9b3b3-432">找到**StoreAsync**方法，然后选择下图中突出显示的代码。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-432">Locate the **StoreAsync** method and select the code highlighted in the following figure.</span></span>

    ![选择代码](maintainable-azure-websites-managing-change-and-scale/_static/image47.png)

    <span data-ttu-id="9b3b3-434">*选择代码*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-434">*Selecting the code*</span></span>
4. <span data-ttu-id="9b3b3-435">右键单击所选代码，展开 "**重构**" 菜单，然后选择 "**提取方法 ...** "。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-435">Right-click the selected code, expand the **Refactor** menu and select **Extract Method...**.</span></span>

    ![将代码提取为新方法](maintainable-azure-websites-managing-change-and-scale/_static/image48.png)

    <span data-ttu-id="9b3b3-437">*选择提取方法*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-437">*Selecting Extract Method*</span></span>
5. <span data-ttu-id="9b3b3-438">在 "**提取方法**" 对话框中，将新方法命名为*MatchesOption* ，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-438">In the **Extract Method** dialog box, name the new method *MatchesOption* and click **OK**.</span></span>

    ![指定方法名称](maintainable-azure-websites-managing-change-and-scale/_static/image49.png)

    <span data-ttu-id="9b3b3-440">*指定提取方法的名称*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-440">*Specifying the name for the extracted method*</span></span>
6. <span data-ttu-id="9b3b3-441">然后，将选定的代码提取到**MatchesOption**方法中。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-441">The selected code is then extracted into the **MatchesOption** method.</span></span> <span data-ttu-id="9b3b3-442">生成的代码将显示在以下代码段中。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-442">The resulting code is shown in the following snippet.</span></span>

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample14.cs)]
7. <span data-ttu-id="9b3b3-443">按**CTRL + S**保存更改。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-443">Press **CTRL + S** to save the changes.</span></span>

<a id="Ex3Task2"></a>
#### <a name="task-2--redeploying-the-geek-quiz-application"></a><span data-ttu-id="9b3b3-444">任务2–重新部署书呆子测验应用程序</span><span class="sxs-lookup"><span data-stu-id="9b3b3-444">Task 2 – Redeploying the Geek Quiz Application</span></span>

<span data-ttu-id="9b3b3-445">你现在将在上一任务中所做的更改推送到存储库，这将触发到生产环境的新部署。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-445">You will now push the changes you made in the previous task to the repository, which will trigger a new deployment to the production environment.</span></span> <span data-ttu-id="9b3b3-446">然后，你将使用 Internet Explorer 提供的**F12 开发工具**对问题进行故障排除，然后从 Azure 管理门户执行到以前的部署的回滚。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-446">Then, you will troubleshot an issue using the **F12 development tools** provided by Internet Explorer, and then perform a rollback to the previous deployment from the Azure management portal.</span></span>

1. <span data-ttu-id="9b3b3-447">打开新的**Git Bash**控制台，将更新的应用程序部署到 Azure App Service。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-447">Open a new **Git Bash** console to deploy the updated application to Azure App Service.</span></span>
2. <span data-ttu-id="9b3b3-448">执行以下命令将更改推送到 Azure。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-448">Execute the following commands to push the changes to Azure.</span></span> <span data-ttu-id="9b3b3-449">将 *[应用程序路径]* 占位符更新为**GeekQuiz**解决方案的路径。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-449">Update the *[YOUR-APPLICATION-PATH]* placeholder with the path to the **GeekQuiz** solution.</span></span> <span data-ttu-id="9b3b3-450">系统将提示你输入部署密码。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-450">You will be prompted for your deployment password.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample15.cmd)]

    ![将重构的代码推送到 Azure](maintainable-azure-websites-managing-change-and-scale/_static/image50.png)

    <span data-ttu-id="9b3b3-452">*将重构的代码推送到 Azure*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-452">*Pushing refactored code to Azure*</span></span>
3. <span data-ttu-id="9b3b3-453">打开 Internet Explorer 并导航到 web 应用（例如 `http://<your-web-site>.azurewebsites.net`）。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-453">Open Internet Explorer and navigate to your web app (e.g. `http://<your-web-site>.azurewebsites.net`).</span></span> <span data-ttu-id="9b3b3-454">使用前面创建的凭据登录。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-454">Log in using the previously created credentials.</span></span>
4. <span data-ttu-id="9b3b3-455">按**F12**启动开发工具，选择 "**网络**" 选项卡，然后单击 "**播放**" 按钮开始录制。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-455">Press **F12** to launch the development tools, select the **Network** tab and click the **Play** button to start recording.</span></span>

    <span data-ttu-id="9b3b3-456">![正在启动网络记录](maintainable-azure-websites-managing-change-and-scale/_static/image51.png "正在启动网络记录")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-456">![Starting network recording](maintainable-azure-websites-managing-change-and-scale/_static/image51.png "Starting network recording")</span></span>

    <span data-ttu-id="9b3b3-457">*正在启动网络记录*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-457">*Starting network recording*</span></span>
5. <span data-ttu-id="9b3b3-458">选择测验的任何选项。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-458">Select any option of the quiz.</span></span> <span data-ttu-id="9b3b3-459">你将看到没有任何反应。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-459">You will see that nothing happens.</span></span>
6. <span data-ttu-id="9b3b3-460">在**F12**窗口中，与 POST http 请求对应的条目显示 HTTP **500**结果。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-460">In the **F12** window, the entry corresponding to the POST HTTP request shows an HTTP **500** result.</span></span>

    ![HTTP 500 错误](maintainable-azure-websites-managing-change-and-scale/_static/image52.png)

    <span data-ttu-id="9b3b3-462">*HTTP 500 错误*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-462">*HTTP 500 error*</span></span>
7. <span data-ttu-id="9b3b3-463">选择 "**控制台**" 选项卡。将记录一个错误，其中包含原因的详细信息。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-463">Select the **Console** tab. An error is logged with the details of the cause.</span></span>

    ![记录的错误](maintainable-azure-websites-managing-change-and-scale/_static/image53.png)

    <span data-ttu-id="9b3b3-465">*记录的错误*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-465">*Logged error*</span></span>
8. <span data-ttu-id="9b3b3-466">找到错误的详细信息部分。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-466">Locate the details part of the error.</span></span> <span data-ttu-id="9b3b3-467">很显然，此错误是由您在前面的步骤中提交的代码重构引起的。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-467">Clearly, this error is caused by the code refactoring you committed in the previous steps.</span></span>

    <span data-ttu-id="9b3b3-468">`Details: LINQ to Entities does not recognize the method 'Boolean MatchesOption ...`。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-468">`Details: LINQ to Entities does not recognize the method 'Boolean MatchesOption ...`.</span></span>
9. <span data-ttu-id="9b3b3-469">不要关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-469">Do not close the browser.</span></span>
10. <span data-ttu-id="9b3b3-470">在新的浏览器实例中，导航到[Azure 管理门户](https://manage.windowsazure.com)，并使用与你的订阅关联的 Microsoft 帐户进行登录。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-470">In a new browser instance, navigate to the [Azure management portal](https://manage.windowsazure.com) and sign in using the Microsoft account associated with your subscription.</span></span>
11. <span data-ttu-id="9b3b3-471">选择 "**网站**"，然后单击在练习2中创建的 web 应用。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-471">Select **Websites** and click the web app you created in Exercise 2.</span></span>
12. <span data-ttu-id="9b3b3-472">导航到 "**部署**" 页。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-472">Navigate to the **Deployments** page.</span></span> <span data-ttu-id="9b3b3-473">请注意，部署历史记录中列出了执行的所有提交。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-473">Notice that all the commits performed are listed in the deployment history.</span></span>

    ![现有部署列表](maintainable-azure-websites-managing-change-and-scale/_static/image54.png)

    <span data-ttu-id="9b3b3-475">*现有部署列表*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-475">*List of existing deployments*</span></span>
13. <span data-ttu-id="9b3b3-476">选择上一个提交，并单击命令栏上的 "重新**部署**"。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-476">Select the previous commit and click **Redeploy** on the command bar.</span></span>

    ![重新部署以前的提交](maintainable-azure-websites-managing-change-and-scale/_static/image55.png)

    <span data-ttu-id="9b3b3-478">*重新部署以前的提交*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-478">*Redeploying the previous commit*</span></span>
14. <span data-ttu-id="9b3b3-479">出现确认提示时，单击“是”。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-479">When prompted to confirm, click **Yes**.</span></span>

    ![确认重新部署](maintainable-azure-websites-managing-change-and-scale/_static/image56.png)
15. <span data-ttu-id="9b3b3-481">部署完成后，请切换回 web 应用的浏览器实例，并按**CTRL + F5**。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-481">When the deployment completes, switch back to the browser instance with your web app and press **CTRL + F5**.</span></span>
16. <span data-ttu-id="9b3b3-482">单击任一选项。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-482">Click any of the options.</span></span> <span data-ttu-id="9b3b3-483">现在，翻转动画将发生，并显示结果（*正确/错误*）。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-483">The flip animation will now take place and the result (*correct/incorrect*) will be displayed.</span></span>
17. <span data-ttu-id="9b3b3-484">可有可无切换到**Git Bash**控制台并执行以下命令以恢复到以前的提交。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-484">(Optional) Switch to the **Git Bash** console and execute the following commands to revert to the previous commit.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9b3b3-485">这些命令将创建一个新的 commit，以撤消在错误提交中进行的 Git 存储库中的所有更改。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-485">These commands create a new commit that undoes all changes in the Git repository that were made in the bad commit.</span></span> <span data-ttu-id="9b3b3-486">然后，Azure 将使用新的提交重新部署应用程序。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-486">Azure will then redeploy the application using the new commit.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample16.cmd)]

<a id="Exercise4"></a>
### <a name="exercise-4-scaling-using-azure-storage"></a><span data-ttu-id="9b3b3-487">练习4：使用 Azure 存储进行缩放</span><span class="sxs-lookup"><span data-stu-id="9b3b3-487">Exercise 4: Scaling Using Azure Storage</span></span>

<span data-ttu-id="9b3b3-488">**Blob**是存储大量非结构化文本或二进制数据（如视频、音频和图像）的最简单方法。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-488">**Blobs** are the simplest way to store large amounts of unstructured text or binary data such as video, audio and images.</span></span> <span data-ttu-id="9b3b3-489">将应用程序的静态内容移动到存储，有助于通过直接向浏览器提供图像或文档来扩展应用程序。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-489">Moving the static content of your application to Storage, helps to scale your application by serving images or documents directly to the browser.</span></span>

<span data-ttu-id="9b3b3-490">在此练习中，你要将应用程序的静态内容移动到 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-490">In this exercise, you will move the static content of your application to a Blob container.</span></span> <span data-ttu-id="9b3b3-491">然后，将应用程序配置为**在 web.config 中**添加**ASP.NET URL 重写规则**，以将内容重定向到 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-491">Then you will configure your application to add an **ASP.NET URL rewrite rule** in the **Web.config** to redirect your content to the Blob container.</span></span>

<a id="Ex4Task1"></a>
#### <a name="task-1--creating-an-azure-storage-account"></a><span data-ttu-id="9b3b3-492">任务1–创建 Azure 存储帐户</span><span class="sxs-lookup"><span data-stu-id="9b3b3-492">Task 1 – Creating an Azure Storage Account</span></span>

<span data-ttu-id="9b3b3-493">在此任务中，你将了解如何使用管理门户创建新的存储帐户。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-493">In this task you will learn how to create a new storage account using the management portal.</span></span>

1. <span data-ttu-id="9b3b3-494">导航到[Azure 管理门户](https://manage.windowsazure.com)，并使用与你的订阅关联的 Microsoft 帐户登录。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-494">Navigate to the [Azure management portal](https://manage.windowsazure.com) and sign in using the Microsoft account associated with your subscription.</span></span>
2. <span data-ttu-id="9b3b3-495">选择**新 |数据服务 |存储 |"快速创建**" 以开始创建新的存储帐户。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-495">Select **New | Data Services | Storage | Quick Create** to start creating a new storage account.</span></span> <span data-ttu-id="9b3b3-496">输入帐户的唯一名称，并从列表中选择一个**区域**。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-496">Enter a unique name for the account and select a **Region** from the list.</span></span> <span data-ttu-id="9b3b3-497">单击 "**创建存储帐户**" 以继续。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-497">Click **Create Storage Account** to continue.</span></span>

    <span data-ttu-id="9b3b3-498">![创建新的存储帐户](maintainable-azure-websites-managing-change-and-scale/_static/image57.png "创建新的存储帐户")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-498">![Creating a new Storage Account](maintainable-azure-websites-managing-change-and-scale/_static/image57.png "Creating a new Storage Account")</span></span>

    <span data-ttu-id="9b3b3-499">*创建新的存储帐户*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-499">*Creating a new storage account*</span></span>
3. <span data-ttu-id="9b3b3-500">在 "**存储**" 部分中，等到新存储帐户的 "状态" 更改为 "*联机*"，才能继续执行以下步骤。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-500">In the **Storage** section, wait until the status of the new storage account changes to *Online* in order to continue with the following step.</span></span>

    <span data-ttu-id="9b3b3-501">![已创建存储帐户](maintainable-azure-websites-managing-change-and-scale/_static/image58.png "已创建存储帐户")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-501">![Storage Account created](maintainable-azure-websites-managing-change-and-scale/_static/image58.png "Storage Account created")</span></span>

    <span data-ttu-id="9b3b3-502">*已创建存储帐户*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-502">*Storage Account created*</span></span>
4. <span data-ttu-id="9b3b3-503">单击存储帐户名称，然后单击页面顶部的 "**仪表板**" 链接。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-503">Click on the storage account name and then click the **Dashboard** link at the top of the page.</span></span> <span data-ttu-id="9b3b3-504">"**仪表板**" 页提供了有关帐户状态和可在应用程序中使用的服务终结点的信息。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-504">The **Dashboard** page provides you with information about the status of the account and the service endpoints that can be used within your applications.</span></span>

    <span data-ttu-id="9b3b3-505">![显示存储帐户仪表板](maintainable-azure-websites-managing-change-and-scale/_static/image59.png "显示存储帐户仪表板")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-505">![Displaying the Storage Account Dashboard](maintainable-azure-websites-managing-change-and-scale/_static/image59.png "Displaying the Storage Account Dashboard")</span></span>

    <span data-ttu-id="9b3b3-506">*显示存储帐户仪表板*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-506">*Displaying the Storage Account Dashboard*</span></span>
5. <span data-ttu-id="9b3b3-507">单击导航栏中的 "**管理访问密钥**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-507">Click the **Manage Access Keys** button in the navigation bar.</span></span>

    <span data-ttu-id="9b3b3-508">!["管理访问密钥" 按钮](maintainable-azure-websites-managing-change-and-scale/_static/image60.png ""管理访问密钥" 按钮")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-508">![Manage Access Keys button](maintainable-azure-websites-managing-change-and-scale/_static/image60.png "Manage Access Keys button")</span></span>

    <span data-ttu-id="9b3b3-509">*"管理访问密钥" 按钮*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-509">*Manage Access Keys button*</span></span>
6. <span data-ttu-id="9b3b3-510">在 "**管理访问密钥**" 对话框中，复制 "**存储帐户名称**" 和 "**主访问密钥**"，因为在以下练习中将需要它们。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-510">In the **Manage Access Keys** dialog box, copy the **Storage Account Name** and **Primary Access Key** as you will need them in the following exercise.</span></span> <span data-ttu-id="9b3b3-511">然后关闭对话框。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-511">Then, close the dialog box.</span></span>

    <span data-ttu-id="9b3b3-512">!["管理访问密钥" 对话框](maintainable-azure-websites-managing-change-and-scale/_static/image61.png ""管理访问密钥" 对话框")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-512">![Manage Access Key dialog box](maintainable-azure-websites-managing-change-and-scale/_static/image61.png "Manage Access Key dialog box")</span></span>

    <span data-ttu-id="9b3b3-513">*"管理访问密钥" 对话框*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-513">*Manage Access Key dialog box*</span></span>

<a id="Ex4Task2"></a>
#### <a name="task-2--uploading-an-asset-to-azure-blob-storage"></a><span data-ttu-id="9b3b3-514">任务 2-将资产上传到 Azure Blob 存储</span><span class="sxs-lookup"><span data-stu-id="9b3b3-514">Task 2 – Uploading an Asset to Azure Blob Storage</span></span>

<span data-ttu-id="9b3b3-515">在此任务中，将使用 Visual Studio 中的 "服务器资源管理器" 窗口连接到存储帐户。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-515">In this task, you will use the Server Explorer window from Visual Studio to connect to your storage account.</span></span> <span data-ttu-id="9b3b3-516">然后，将创建一个 blob 容器，并将带有书呆子测验徽标的文件上传到该容器。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-516">You will then create a blob container and upload a file with the Geek Quiz logo to the container.</span></span>

1. <span data-ttu-id="9b3b3-517">切换到 Visual Studio 实例，其中包含上一练习中的**GeekQuiz**解决方案。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-517">Switch to the Visual Studio instance with the **GeekQuiz** solution from the previous exercise.</span></span>
2. <span data-ttu-id="9b3b3-518">从菜单栏中选择 "**视图**"，然后单击 "**服务器资源管理器**"。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-518">From the menu bar, select **View** and then click **Server Explorer**.</span></span>
3. <span data-ttu-id="9b3b3-519">在**服务器资源管理器**中，右键单击**Azure**节点，并选择 "**连接到 Azure ...** "。使用与你的订阅关联的 Microsoft 帐户登录。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-519">In **Server Explorer**, right-click the **Azure** node and select **Connect to Azure...**. Sign in using the Microsoft account associated with your subscription.</span></span>

    ![连接到 Windows Azure](maintainable-azure-websites-managing-change-and-scale/_static/image62.png)

    <span data-ttu-id="9b3b3-521">*连接到 Azure*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-521">*Connect to Azure*</span></span>
4. <span data-ttu-id="9b3b3-522">展开 " **Azure** " 节点，右键单击 "**存储**"，然后选择 "**附加外部存储 ...** "。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-522">Expand the **Azure** node, right-click **Storage** and select **Attach External Storage...**.</span></span>
5. <span data-ttu-id="9b3b3-523">在 "**添加新存储帐户**" 对话框中，输入你在上一任务中获取的**帐户名称**和**帐户密钥**，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-523">In the **Add New Storage Account** dialog box, enter the **Account name** and **Account key** you obtained in the previous task and click **OK**.</span></span>

    !["添加新存储帐户" 对话框](maintainable-azure-websites-managing-change-and-scale/_static/image63.png)

    <span data-ttu-id="9b3b3-525">*"添加新存储帐户" 对话框*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-525">*Add New Storage Account dialog box*</span></span>
6. <span data-ttu-id="9b3b3-526">存储帐户应该出现在 "**存储**" 节点下。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-526">Your storage account should appear under the **Storage** node.</span></span> <span data-ttu-id="9b3b3-527">展开存储帐户，右键单击 " **blob** "，然后选择 "**创建 Blob 容器 ...** "。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-527">Expand your storage account, right-click **Blobs** and select **Create Blob Container...**.</span></span>

    <span data-ttu-id="9b3b3-528">![创建 Blob 容器](maintainable-azure-websites-managing-change-and-scale/_static/image64.png "创建 Blob 容器")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-528">![Create Blob Container](maintainable-azure-websites-managing-change-and-scale/_static/image64.png "Create Blob Container")</span></span>

    <span data-ttu-id="9b3b3-529">*创建 Blob 容器*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-529">*Create Blob Container*</span></span>
7. <span data-ttu-id="9b3b3-530">在 "**创建 Blob 容器**" 对话框中，输入 Blob 容器的名称，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-530">In the **Create Blob Container** dialog box, enter a name for the blob container and click **OK**.</span></span>

    <span data-ttu-id="9b3b3-531">!["创建 Blob 容器" 对话框](maintainable-azure-websites-managing-change-and-scale/_static/image65.png ""创建 Blob 容器" 对话框")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-531">![Create Blob Container dialog box](maintainable-azure-websites-managing-change-and-scale/_static/image65.png "Create Blob Container dialog box")</span></span>

    <span data-ttu-id="9b3b3-532">*"创建 Blob 容器" 对话框*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-532">*Create Blob Container dialog box*</span></span>
8. <span data-ttu-id="9b3b3-533">应将新的 blob 容器添加到**blob**节点。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-533">The new blob container should be added to the **Blobs** node.</span></span> <span data-ttu-id="9b3b3-534">更改容器中的访问权限，使容器成为公共容器。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-534">Change the access permissions in the container to make the container public.</span></span> <span data-ttu-id="9b3b3-535">为此，请右键单击**images**容器，然后选择 "**属性**"。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-535">To do this, right-click the **images** container and select **Properties**.</span></span>

    <span data-ttu-id="9b3b3-536">![图像容器属性](maintainable-azure-websites-managing-change-and-scale/_static/image66.png "图像容器属性")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-536">![images container properties](maintainable-azure-websites-managing-change-and-scale/_static/image66.png "images container properties")</span></span>

    <span data-ttu-id="9b3b3-537">*图像容器属性*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-537">*Images container properties*</span></span>
9. <span data-ttu-id="9b3b3-538">在 "**属性**" 窗口中，将 "**公共读取访问权限**" 设置为 "**容器**"。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-538">In the **Properties** window, set the **Public Read Access** to **Container**.</span></span>

    <span data-ttu-id="9b3b3-539">![更改公共读取访问属性](maintainable-azure-websites-managing-change-and-scale/_static/image67.png "更改公共读取访问属性")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-539">![Changing public read access property](maintainable-azure-websites-managing-change-and-scale/_static/image67.png "Changing public read access property")</span></span>

    <span data-ttu-id="9b3b3-540">*更改公共读取访问属性*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-540">*Changing public read access property*</span></span>
10. <span data-ttu-id="9b3b3-541">当系统提示你是否确定要更改公共访问属性时，请单击 **"是"** 。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-541">When prompted if you are sure you want to change the public access property, click **Yes**.</span></span>

    <span data-ttu-id="9b3b3-542">![Microsoft Visual Studio 警告](maintainable-azure-websites-managing-change-and-scale/_static/image68.png "Microsoft Visual Studio 警告")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-542">![Microsoft Visual Studio warning](maintainable-azure-websites-managing-change-and-scale/_static/image68.png "Microsoft Visual Studio warning")</span></span>

    <span data-ttu-id="9b3b3-543">*Microsoft Visual Studio 警告*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-543">*Microsoft Visual Studio warning*</span></span>
11. <span data-ttu-id="9b3b3-544">在**服务器资源管理器**中，右键单击**images** blob 容器，然后选择 "**查看 blob 容器**"。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-544">In **Server Explorer**, right-click in the **images** blob container and select **View Blob Container**.</span></span>

    <span data-ttu-id="9b3b3-545">![查看 Blob 容器](maintainable-azure-websites-managing-change-and-scale/_static/image69.png "查看 Blob 容器")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-545">![View Blob Container](maintainable-azure-websites-managing-change-and-scale/_static/image69.png "View Blob Container")</span></span>

    <span data-ttu-id="9b3b3-546">*查看 Blob 容器*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-546">*View Blob Container*</span></span>
12. <span data-ttu-id="9b3b3-547">图像容器应在新窗口中打开，并且应显示不含任何条目的图例。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-547">The images container should open in a new window and a legend with no entries should be shown.</span></span> <span data-ttu-id="9b3b3-548">单击 "**上传**" 图标，将文件上传到 blob 容器。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-548">Click the **upload** icon to upload a file to the blob container.</span></span>

    <span data-ttu-id="9b3b3-549">![没有条目的图像容器](maintainable-azure-websites-managing-change-and-scale/_static/image70.png "没有条目的图像容器")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-549">![Images container with no entries](maintainable-azure-websites-managing-change-and-scale/_static/image70.png "Images container with no entries")</span></span>

    <span data-ttu-id="9b3b3-550">*没有条目的图像容器*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-550">*Images container with no entries*</span></span>
13. <span data-ttu-id="9b3b3-551">在 "**上传 Blob** " 对话框中，导航到实验室的 "**资产**" 文件夹。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-551">In the **Upload Blob** dialog box, navigate to the **Assets** folder of the lab.</span></span> <span data-ttu-id="9b3b3-552">选择**logo-big**文件并单击 "**打开**"。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-552">Select the **logo-big.png** file and click **Open**.</span></span>
14. <span data-ttu-id="9b3b3-553">等待文件上传。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-553">Wait until the file is uploaded.</span></span> <span data-ttu-id="9b3b3-554">上传完成后，该文件应在 images 容器中列出。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-554">When the upload completes, the file should be listed in the images container.</span></span> <span data-ttu-id="9b3b3-555">右键单击该文件条目，然后选择 "**复制 URL**"。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-555">Right-click the file entry and select **Copy URL**.</span></span>

    <span data-ttu-id="9b3b3-556">![复制 blob URL](maintainable-azure-websites-managing-change-and-scale/_static/image71.png "复制 blob 文件 URL")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-556">![Copy blob URL](maintainable-azure-websites-managing-change-and-scale/_static/image71.png "Copy blob file URL")</span></span>

    <span data-ttu-id="9b3b3-557">*复制 blob URL*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-557">*Copy blob URL*</span></span>
15. <span data-ttu-id="9b3b3-558">打开 Internet Explorer 并粘贴 URL。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-558">Open Internet Explorer and paste the URL.</span></span> <span data-ttu-id="9b3b3-559">以下图像应显示在浏览器中。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-559">The following image should be shown in the browser.</span></span>

    <span data-ttu-id="9b3b3-560">![Windows Blob 存储中的 logo-big 映像](maintainable-azure-websites-managing-change-and-scale/_static/image72.png "logo-big 存储中的 .png 映像")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-560">![logo-big.png image from Windows Blob Storage](maintainable-azure-websites-managing-change-and-scale/_static/image72.png "logo-big.png image from storage")</span></span>

    <span data-ttu-id="9b3b3-561">*Azure Blob 存储中的 logo-big 映像*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-561">*logo-big.png image from Azure Blob Storage*</span></span>

<a id="Ex4Task3"></a>
#### <a name="task-3--updating-the-solution-to-consume-static-content-from-azure-blob-storage"></a><span data-ttu-id="9b3b3-562">任务3–更新解决方案以使用 Azure Blob 存储中的静态内容</span><span class="sxs-lookup"><span data-stu-id="9b3b3-562">Task 3 – Updating the Solution to Consume Static Content from Azure Blob Storage</span></span>

<span data-ttu-id="9b3b3-563">在此任务中，你将配置**GeekQuiz**解决方案，以使用上传到 Azure Blob 存储（而不是位于 web 应用中的映像）的图像，方法是在**web.config 文件中**添加 ASP.NET URL 重写规则。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-563">In this task, you will configure the **GeekQuiz** solution to consume the image uploaded to Azure Blob Storage (instead of the image located in the web app) by adding an ASP.NET URL rewrite rule in the **web.config** file.</span></span>

1. <span data-ttu-id="9b3b3-564">在 Visual Studio 中，打开**GeekQuiz**项目**中的 web.config 文件，** 并找到 **&lt;system.webserver&gt;** 元素。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-564">In Visual Studio, open the **Web.config** file inside the **GeekQuiz** project and locate the **&lt;system.webServer&gt;** element.</span></span>
2. <span data-ttu-id="9b3b3-565">添加以下代码以添加 URL 重写规则，并使用您的存储帐户名称更新占位符。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-565">Add the following code to add an URL rewrite rule, updating the placeholder with your storage account name.</span></span>

    <span data-ttu-id="9b3b3-566">（代码段- *WebSitesInProduction-Ex4-UrlRewriteRule*）</span><span class="sxs-lookup"><span data-stu-id="9b3b3-566">(Code Snippet - *WebSitesInProduction - Ex4 - UrlRewriteRule*)</span></span>

    [!code-xml[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample17.xml)]

    > [!NOTE]
    > <span data-ttu-id="9b3b3-567">URL 重写是拦截传入的 Web 请求并将请求重定向到其他资源的过程。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-567">URL rewriting is the process of intercepting an incoming Web request and redirecting the request to a different resource.</span></span> <span data-ttu-id="9b3b3-568">URL 重写规则告诉重写引擎何时需要重定向请求，以及应重定向到的位置。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-568">The URL rewriting rules tells the rewriting engine when a request needs to be redirected, and where should they be redirected.</span></span> <span data-ttu-id="9b3b3-569">重写规则由以下两个字符串组成：要在请求的 URL 中查找的模式（通常使用正则表达式）和替换模式的字符串（如果找到）。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-569">A rewriting rule is composed of two strings: the pattern to look for in the requested URL (usually, using regular expressions), and the string to replace the pattern with, if found.</span></span> <span data-ttu-id="9b3b3-570">有关详细信息，请参阅[ASP.NET 中的 URL 重写](https://msdn.microsoft.com/library/ms972974.aspx)。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-570">For more information, see [URL Rewriting in ASP.NET](https://msdn.microsoft.com/library/ms972974.aspx).</span></span>
3. <span data-ttu-id="9b3b3-571">按**CTRL + S**保存更改。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-571">Press **CTRL + S** to save the changes.</span></span>
4. <span data-ttu-id="9b3b3-572">打开新的**Git Bash**控制台，将更新的应用程序部署到 Azure App Service。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-572">Open a new **Git Bash** console to deploy the updated application to Azure App Service.</span></span>
5. <span data-ttu-id="9b3b3-573">执行以下命令将更改推送到 Azure。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-573">Execute the following commands to push the changes to Azure.</span></span> <span data-ttu-id="9b3b3-574">将 *[应用程序路径]* 占位符更新为**GeekQuiz**解决方案的路径。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-574">Update the *[YOUR-APPLICATION-PATH]* placeholder with the path to the **GeekQuiz** solution.</span></span> <span data-ttu-id="9b3b3-575">系统将提示你输入部署密码。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-575">You will be prompted for your deployment password.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample18.cmd)]

    ![将更新部署到 Azure](maintainable-azure-websites-managing-change-and-scale/_static/image73.png)

    <span data-ttu-id="9b3b3-577">*将更新部署到 Azure*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-577">*Deploying update to Azure*</span></span>

<a id="Ex4Task4"></a>
#### <a name="task-4--verification"></a><span data-ttu-id="9b3b3-578">任务 4 – 验证</span><span class="sxs-lookup"><span data-stu-id="9b3b3-578">Task 4 – Verification</span></span>

<span data-ttu-id="9b3b3-579">在此任务中，你将使用**Internet Explorer**来浏览**书呆子测验**应用程序，并检查图像的 URL 重写规则是否正常工作，以及你是否已重定向到**Azure Blob 存储**上托管的映像。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-579">In this task you will use **Internet Explorer** to browse the **Geek Quiz** application and check that the URL rewrite rule for images works and you are redirected to the image hosted on **Azure Blob Storage**.</span></span>

1. <span data-ttu-id="9b3b3-580">打开 Internet Explorer 并导航到 web 应用（例如 `http://<your-web-site>.azurewebsites.net`）。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-580">Open Internet Explorer and navigate to your web app (e.g. `http://<your-web-site>.azurewebsites.net`).</span></span> <span data-ttu-id="9b3b3-581">使用前面创建的凭据登录。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-581">Log in using the previously created credentials.</span></span>

    <span data-ttu-id="9b3b3-582">![显示包含图像的书呆子测验 web 应用](maintainable-azure-websites-managing-change-and-scale/_static/image74.png "显示包含图像的书呆子测验 web 应用")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-582">![Showing the Geek Quiz web app with the image](maintainable-azure-websites-managing-change-and-scale/_static/image74.png "Showing the Geek Quiz web app with the image")</span></span>

    <span data-ttu-id="9b3b3-583">*显示包含图像的书呆子测验 web 应用*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-583">*Showing the Geek Quiz web app with the image*</span></span>
2. <span data-ttu-id="9b3b3-584">按**F12**启动开发工具，选择 "**网络**" 选项卡并开始记录。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-584">Press **F12** to launch the development tools, select the **Network** tab and start recording.</span></span>

    <span data-ttu-id="9b3b3-585">![正在启动网络记录](maintainable-azure-websites-managing-change-and-scale/_static/image75.png "正在启动网络记录")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-585">![Starting network recording](maintainable-azure-websites-managing-change-and-scale/_static/image75.png "Starting network recording")</span></span>

    <span data-ttu-id="9b3b3-586">*正在启动网络记录*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-586">*Starting network recording*</span></span>
3. <span data-ttu-id="9b3b3-587">按**CTRL + F5**刷新网页。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-587">Press **CTRL + F5** to refresh the web page.</span></span>
4. <span data-ttu-id="9b3b3-588">页面加载完成后，应会看到 **/Img/logo-big.png** url 发出 http 请求，其中包含 http **301**结果（重定向），另一请求使用 HTTP **200**结果 `http://[YOUR-STORAGE-ACCOUNT].blob.core.windows.net/images/logo-big.png` url。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-588">Once the page has finished loading, you should see an HTTP request for the **/img/logo-big.png** URL with an HTTP **301** result (redirect) and another request for `http://[YOUR-STORAGE-ACCOUNT].blob.core.windows.net/images/logo-big.png` URL with a HTTP **200** result.</span></span>

    <span data-ttu-id="9b3b3-589">![验证 URL 重定向](maintainable-azure-websites-managing-change-and-scale/_static/image76.png "在开发工具中显示重定向")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-589">![Verifying the URL redirect](maintainable-azure-websites-managing-change-and-scale/_static/image76.png "Showing the redirect in Dev Tools")</span></span>

    <span data-ttu-id="9b3b3-590">*验证 URL 重定向*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-590">*Verifying the URL redirect*</span></span>

<a id="Exercise5"></a>
### <a name="exercise-5-using-autoscale-for-web-apps"></a><span data-ttu-id="9b3b3-591">练习5：对 Web 应用使用自动缩放</span><span class="sxs-lookup"><span data-stu-id="9b3b3-591">Exercise 5: Using Autoscale for Web Apps</span></span>

> [!NOTE]
> <span data-ttu-id="9b3b3-592">此练习是可选的，因为它需要支持 Web 负载 &amp; 仅适用于**Visual Studio 2013 旗舰版**的性能测试。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-592">This exercise is optional, since it requires support for Web Load &amp; Performance Testing which is only available for **Visual Studio 2013 Ultimate Edition**.</span></span> <span data-ttu-id="9b3b3-593">有关特定 Visual Studio 2013 功能的详细信息，请在[此处](https://www.microsoft.com/visualstudio/eng/products/compare)比较版本。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-593">For more information on specific Visual Studio 2013 features, compare versions [here](https://www.microsoft.com/visualstudio/eng/products/compare).</span></span>

<span data-ttu-id="9b3b3-594">**Azure App Service Web apps**为在 "**标准" 模式下**运行的 Web 应用提供自动缩放功能。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-594">**Azure App Service Web Apps** provides the Autoscale feature for web apps running in **Standard Mode**.</span></span> <span data-ttu-id="9b3b3-595">自动缩放可让 Azure 根据负载自动缩放 web 应用的实例计数。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-595">Autoscale lets Azure automatically scale the instance count of your web app depending on the load.</span></span> <span data-ttu-id="9b3b3-596">启用自动缩放后，Azure 每五分钟检查一次 web 应用的 CPU，并根据需要在该时间点添加实例。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-596">When Autoscale is enabled, Azure checks the CPU of your web app once every five minutes and adds instances as needed at that point in time.</span></span> <span data-ttu-id="9b3b3-597">如果 CPU 使用率较低，Azure 将每两小时删除一次实例，以确保 web 应用的性能不会下降。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-597">If the CPU usage is low, Azure will remove instances once every two hours to ensure that the performance of your web app is not degraded.</span></span>

<span data-ttu-id="9b3b3-598">在本练习中，你将完成配置**书呆子测验**web 应用的**自动缩放**功能所需的步骤。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-598">In this exercise you will go through the steps required to configure the **Autoscale** feature for the **Geek Quiz** web app.</span></span> <span data-ttu-id="9b3b3-599">你将通过运行 Visual Studio 负载测试来验证此功能，以便在应用程序上生成足够的 CPU 负载以触发实例升级。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-599">You will verify this feature by running a Visual Studio load test to generate enough CPU load on the application to trigger an instance upgrade.</span></span>

<a id="Ex5Task1"></a>
#### <a name="task-1--configuring-autoscale-based-on-the-cpu-metric"></a><span data-ttu-id="9b3b3-600">任务1–基于 CPU 指标配置自动缩放</span><span class="sxs-lookup"><span data-stu-id="9b3b3-600">Task 1 – Configuring Autoscale Based on the CPU Metric</span></span>

<span data-ttu-id="9b3b3-601">在此任务中，你将使用 Azure 管理门户为在练习2中创建的 web 应用启用自动缩放功能。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-601">In this task you will use the Azure management portal to enable the Autoscale feature for the web app you created in Exercise 2.</span></span>

1. <span data-ttu-id="9b3b3-602">在[Azure 管理门户](https://manage.windowsazure.com/)中，选择 "**网站**"，然后单击在练习2中创建的 web 应用。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-602">In the [Azure management portal](https://manage.windowsazure.com/), select **Websites** and click the web app you created in Exercise 2.</span></span>
2. <span data-ttu-id="9b3b3-603">导航到 "**缩放**" 页。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-603">Navigate to the **Scale** page.</span></span> <span data-ttu-id="9b3b3-604">在 "**容量**" 部分下，为 "**按度量值缩放**" 配置选择 " **CPU** "。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-604">Under the **capacity** section, select **CPU** for the **Scale by Metric** configuration.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9b3b3-605">按 CPU 进行缩放时，Azure 会动态调整应用在 CPU 使用率变化时使用的实例数。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-605">When scaling by CPU, Azure dynamically adjusts the number of instances that the app uses if the CPU usage changes.</span></span>

    <span data-ttu-id="9b3b3-606">![选择按 CPU 进行缩放](maintainable-azure-websites-managing-change-and-scale/_static/image77.png "选择自动缩放的 CPU 指标")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-606">![Selecting to scale by CPU](maintainable-azure-websites-managing-change-and-scale/_static/image77.png "Selecting the CPU metric for auto scaling")</span></span>

    <span data-ttu-id="9b3b3-607">*选择按 CPU 进行缩放*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-607">*Selecting to scale by CPU*</span></span>
3. <span data-ttu-id="9b3b3-608">将**目标 CPU**配置更改为**20**-**40** %。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-608">Change the **Target CPU** configuration to **20**-**40** percent.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9b3b3-609">此范围表示 web 应用的平均 CPU 使用率。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-609">This range represents the average CPU usage for your web app.</span></span> <span data-ttu-id="9b3b3-610">Azure 将添加或删除实例，以使你的 web 应用保持在此范围中。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-610">Azure will add or remove instances to keep your web app in this range.</span></span> <span data-ttu-id="9b3b3-611">用于缩放的最小和最大实例数是在**实例计数**配置中指定的。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-611">The minimum and maximum number of instances used for scaling is specified in the **Instance Count** configuration.</span></span> <span data-ttu-id="9b3b3-612">Azure 绝不会超出或超出该限制。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-612">Azure will never go above or beyond that limit.</span></span>
    >
    > <span data-ttu-id="9b3b3-613">默认情况下，仅为此实验室修改默认**目标 CPU**值。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-613">The default **Target CPU** values are modified just for the purposes of this lab.</span></span> <span data-ttu-id="9b3b3-614">通过使用较小的值配置 CPU 范围，可以增加在应用程序上放置了中等负载时触发自动缩放的机会。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-614">By configuring the CPU range with small values, you are increasing the chances to trigger Autoscale when a moderate load is placed on the application.</span></span>

    <span data-ttu-id="9b3b3-615">![将目标 CPU 更改为20% 到40%](maintainable-azure-websites-managing-change-and-scale/_static/image78.png "将目标 CPU 更改为20% 到40%")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-615">![Changing the target CPU to be between 20 and 40 percent](maintainable-azure-websites-managing-change-and-scale/_static/image78.png "Changing the target CPU to be between 20 and 40 percent")</span></span>

    <span data-ttu-id="9b3b3-616">*将目标 CPU 更改为20% 到40%*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-616">*Changing the Target CPU to be between 20 and 40 percent*</span></span>
4. <span data-ttu-id="9b3b3-617">单击命令栏中的 "**保存**" 以保存更改。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-617">Click **Save** in the command bar to save the changes.</span></span>

<a id="Ex5Task2"></a>
#### <a name="task-2--load-testing-with-visual-studio"></a><span data-ttu-id="9b3b3-618">任务 2-通过 Visual Studio 进行负载测试</span><span class="sxs-lookup"><span data-stu-id="9b3b3-618">Task 2 – Load Testing with Visual Studio</span></span>

<span data-ttu-id="9b3b3-619">现在已配置**自动缩放**，你将在 Visual Studio 中创建**Web 性能和负载测试项目**，以在 Web 应用上生成一些 CPU 负载。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-619">Now that **Autoscale** has been configured, you will create a **Web Performance and Load Test Project** in Visual Studio to generate some CPU load on your web app.</span></span>

1. <span data-ttu-id="9b3b3-620">打开**Visual Studio Ultimate 2013** ，然后选择 "**文件" |新建 |项目 ...** 启动新解决方案。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-620">Open **Visual Studio Ultimate 2013** and select **File | New | Project...** to start a new solution.</span></span>

    <span data-ttu-id="9b3b3-621">![创建新项目](maintainable-azure-websites-managing-change-and-scale/_static/image79.png "创建新的项目")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-621">![Creating a new project](maintainable-azure-websites-managing-change-and-scale/_static/image79.png "Creating a new project")</span></span>

    <span data-ttu-id="9b3b3-622">*创建新项目*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-622">*Creating a new project*</span></span>
2. <span data-ttu-id="9b3b3-623">在 "**新建项目**" 对话框中，选择 " **Web 性能和负载测试项目**"。  **C#** 请确保选择 **.NET Framework 4.5** ，将项目命名为*WebAndLoadTestProject*，选择一个**位置**，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-623">In the **New Project** dialog box, select **Web Performance and Load Test Project** under the **Visual C# | Test** tab. Make sure **.NET Framework 4.5** is selected, name the project *WebAndLoadTestProject*, choose a **Location** and click **OK**.</span></span>

    <span data-ttu-id="9b3b3-624">![创建新的 Web 和负载测试项目](maintainable-azure-websites-managing-change-and-scale/_static/image80.png "创建新的 Web 和负载测试项目")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-624">![Creating a new Web and Load Test project](maintainable-azure-websites-managing-change-and-scale/_static/image80.png "Creating a new Web and Load Test project")</span></span>

    <span data-ttu-id="9b3b3-625">*创建新的 Web 和负载测试项目*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-625">*Creating a new Web and Load Test project*</span></span>
3. <span data-ttu-id="9b3b3-626">在**webtest1.webtest**中，右键单击**webtest1.webtest**节点，然后单击 "**添加请求**"。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-626">In the **WebTest1.webtest** Right-click the **WebTest1** node and click **Add Request**.</span></span>

    <span data-ttu-id="9b3b3-627">![向 Webtest1.webtest 添加请求](maintainable-azure-websites-managing-change-and-scale/_static/image81.png "向 Webtest1.webtest 添加请求")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-627">![Adding a request to WebTest1](maintainable-azure-websites-managing-change-and-scale/_static/image81.png "Adding a request to WebTest1")</span></span>

    <span data-ttu-id="9b3b3-628">*向 Webtest1.webtest 添加请求*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-628">*Adding a request to WebTest1*</span></span>
4. <span data-ttu-id="9b3b3-629">在新请求节点的 "**属性**" 窗口中，将 " **url** " 属性更新为指向 web 应用的 url （例如 *[http://geek-quiz.azurewebsites.net/](http://geek-quiz.azurewebsites.net/)* ）。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-629">In the **Properties** window of the new request node, update the **Url** property to point to the URL of your web app (e.g. *[http://geek-quiz.azurewebsites.net/](http://geek-quiz.azurewebsites.net/)*).</span></span>

    <span data-ttu-id="9b3b3-630">![更改 Url 属性](maintainable-azure-websites-managing-change-and-scale/_static/image82.png "更改 Url 属性")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-630">![Changing the Url property](maintainable-azure-websites-managing-change-and-scale/_static/image82.png "Changing the Url property")</span></span>

    <span data-ttu-id="9b3b3-631">*更改 Url 属性*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-631">*Changing the Url property*</span></span>
5. <span data-ttu-id="9b3b3-632">在**webtest1.webtest webtest**窗口中，右键单击**webtest1.webtest** ，然后单击 "**添加循环 ...** "。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-632">In the **WebTest1.webtest** window, right-click **WebTest1** and click **Add Loop...**.</span></span>

    <span data-ttu-id="9b3b3-633">![向 Webtest1.webtest 添加循环](maintainable-azure-websites-managing-change-and-scale/_static/image83.png "向 Webtest1.webtest 添加循环")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-633">![Adding a loop to WebTest1](maintainable-azure-websites-managing-change-and-scale/_static/image83.png "Adding a loop to WebTest1")</span></span>

    <span data-ttu-id="9b3b3-634">*向 Webtest1.webtest 添加循环*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-634">*Adding a loop to WebTest1*</span></span>
6. <span data-ttu-id="9b3b3-635">在 "**添加条件规则" 和 "要循环的项**" 对话框中，选择**for 循环**规则并修改以下属性。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-635">In the **Add Conditional Rule and Items to Loop** dialog box, select the **For Loop** rule and modify the following properties.</span></span>

   1. <span data-ttu-id="9b3b3-636">**终止值：** 1000</span><span class="sxs-lookup"><span data-stu-id="9b3b3-636">**Terminating value:** 1000</span></span>
   2. <span data-ttu-id="9b3b3-637">**上下文参数名称：** 器</span><span class="sxs-lookup"><span data-stu-id="9b3b3-637">**Context Parameter Name:** Iterator</span></span>
   3. <span data-ttu-id="9b3b3-638">**增量值：** 1</span><span class="sxs-lookup"><span data-stu-id="9b3b3-638">**Increment Value:** 1</span></span>

      <span data-ttu-id="9b3b3-639">![选择 For 循环规则并更新属性](maintainable-azure-websites-managing-change-and-scale/_static/image84.png "选择 For 循环规则并更新属性")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-639">![Selecting the For Loop rule and updating the properties](maintainable-azure-websites-managing-change-and-scale/_static/image84.png "Selecting the For Loop rule and updating the properties")</span></span>

      <span data-ttu-id="9b3b3-640">*选择 For 循环规则并更新属性*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-640">*Selecting the For Loop rule and updating the properties*</span></span>
7. <span data-ttu-id="9b3b3-641">在 "**循环中的项**" 部分下，选择之前创建的请求作为该循环的第一项和最后一项。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-641">Under the **Items in loop** section, select the request you created previously to be the first and last item for the loop.</span></span> <span data-ttu-id="9b3b3-642">单击 **“确定”** 继续。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-642">Click **OK** to continue.</span></span>

    <span data-ttu-id="9b3b3-643">![选择循环的第一项和最后一项](maintainable-azure-websites-managing-change-and-scale/_static/image85.png "选择循环的第一项和最后一项")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-643">![Selecting the first and last items for the loop](maintainable-azure-websites-managing-change-and-scale/_static/image85.png "Selecting the first and last items for the loop")</span></span>

    <span data-ttu-id="9b3b3-644">*选择循环的第一项和最后一项*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-644">*Selecting the first and last items for the loop*</span></span>
8. <span data-ttu-id="9b3b3-645">在**解决方案资源管理器**中，右键单击**WebAndLoadTestProject**项目，展开 "**添加**" 菜单，然后选择 "**负载测试 ...** "。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-645">In **Solution Explorer**, right-click the **WebAndLoadTestProject** project, expand the **Add** menu and select **Load Test...**.</span></span>

    <span data-ttu-id="9b3b3-646">![将负载测试添加到 WebAndLoadTestProject 项目](maintainable-azure-websites-managing-change-and-scale/_static/image86.png "将负载测试添加到 WebAndLoadTestProject 项目")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-646">![Adding a Load Test to the WebAndLoadTestProject project](maintainable-azure-websites-managing-change-and-scale/_static/image86.png "Adding a Load Test to the WebAndLoadTestProject project")</span></span>

    <span data-ttu-id="9b3b3-647">*将负载测试添加到 WebAndLoadTestProject 项目*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-647">*Adding a Load Test to the WebAndLoadTestProject project*</span></span>
9. <span data-ttu-id="9b3b3-648">在 "**新建负载测试向导**" 对话框中，单击 "**下一步**"。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-648">In the **New Load Test Wizard** dialog box, click **Next**.</span></span>

    <span data-ttu-id="9b3b3-649">![新负载测试向导](maintainable-azure-websites-managing-change-and-scale/_static/image87.png "新负载测试向导")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-649">![New Load Test Wizard](maintainable-azure-websites-managing-change-and-scale/_static/image87.png "New Load Test Wizard")</span></span>

    <span data-ttu-id="9b3b3-650">*新负载测试向导*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-650">*New Load Test Wizard*</span></span>
10. <span data-ttu-id="9b3b3-651">在 "**方案**" 页上，选择 "**不使用思考时间**"，然后单击 "**下一步**"。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-651">In the **Scenario** page, select **Do not use think times** and click **Next**.</span></span>

    <span data-ttu-id="9b3b3-652">![选择不使用思考时间](maintainable-azure-websites-managing-change-and-scale/_static/image88.png "选择不使用思考时间")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-652">![Selecting not to use think times](maintainable-azure-websites-managing-change-and-scale/_static/image88.png "Selecting not to use think times")</span></span>

    <span data-ttu-id="9b3b3-653">*选择不使用思考时间*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-653">*Selecting not to use think times*</span></span>
11. <span data-ttu-id="9b3b3-654">在 "**负载模式**" 页上，确保选择 "**常量加载**" 选项。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-654">In the **Load Pattern** page, make sure that the **Constant Load** option is selected.</span></span> <span data-ttu-id="9b3b3-655">将**用户计数**设置更改为**250**用户，然后单击 "**下一步**"。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-655">Change the **User Count** setting to **250** users and click **Next**.</span></span>

    <span data-ttu-id="9b3b3-656">![将用户计数更改为250](maintainable-azure-websites-managing-change-and-scale/_static/image89.png "将用户计数更改为250")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-656">![Changing the user count to 250](maintainable-azure-websites-managing-change-and-scale/_static/image89.png "Changing the user count to 250")</span></span>

    <span data-ttu-id="9b3b3-657">*将用户计数更改为250*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-657">*Changing the user count to 250*</span></span>
12. <span data-ttu-id="9b3b3-658">在 "**测试组合模型**" 页中，选择 "**基于顺序测试顺序**"，然后单击 "**下一步**"。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-658">In the **Test Mix Model** page, select **Based on sequential test order** and click **Next**.</span></span>

    <span data-ttu-id="9b3b3-659">![选择测试组合模型](maintainable-azure-websites-managing-change-and-scale/_static/image90.png "选择测试组合模型")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-659">![Selecting the test mix model](maintainable-azure-websites-managing-change-and-scale/_static/image90.png "Selecting the test mix model")</span></span>

    <span data-ttu-id="9b3b3-660">*选择测试组合模型*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-660">*Selecting the test mix model*</span></span>
13. <span data-ttu-id="9b3b3-661">在 "**测试组合模型**" 页中，单击 "**添加 ...** " 将测试添加到组合。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-661">In the **Test Mix Model** page, click **Add...** to add a test to the mix.</span></span>

    <span data-ttu-id="9b3b3-662">![向测试组合中添加测试](maintainable-azure-websites-managing-change-and-scale/_static/image91.png "向测试组合中添加测试")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-662">![Adding a test to the test mix](maintainable-azure-websites-managing-change-and-scale/_static/image91.png "Adding a test to the test mix")</span></span>

    <span data-ttu-id="9b3b3-663">*向测试组合中添加测试*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-663">*Adding a test to the test mix*</span></span>
14. <span data-ttu-id="9b3b3-664">在 "**添加测试**" 对话框中，双击 " **webtest1.webtest** " 将测试添加到 "**选定的测试**" 列表。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-664">In the **Add Tests** dialog box, double-click **WebTest1** to add the test to the **Selected tests** list.</span></span> <span data-ttu-id="9b3b3-665">单击 **“确定”** 继续。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-665">Click **OK** to continue.</span></span>

    <span data-ttu-id="9b3b3-666">![添加 Webtest1.webtest 测试](maintainable-azure-websites-managing-change-and-scale/_static/image92.png "添加 Webtest1.webtest 测试")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-666">![Adding the WebTest1 test](maintainable-azure-websites-managing-change-and-scale/_static/image92.png "Adding the WebTest1 test")</span></span>

    <span data-ttu-id="9b3b3-667">*添加 Webtest1.webtest 测试*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-667">*Adding the WebTest1 test*</span></span>
15. <span data-ttu-id="9b3b3-668">返回到**测试组合**页，单击 "**下一步**"。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-668">Back in the **Test Mix** page, click **Next**.</span></span>

    <span data-ttu-id="9b3b3-669">![完成测试组合页](maintainable-azure-websites-managing-change-and-scale/_static/image93.png "完成测试组合页")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-669">![Completing the Test Mix page](maintainable-azure-websites-managing-change-and-scale/_static/image93.png "Completing the Test Mix page")</span></span>

    <span data-ttu-id="9b3b3-670">*完成测试组合页*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-670">*Completing the Test Mix page*</span></span>
16. <span data-ttu-id="9b3b3-671">在 "**网络组合**" 页上，单击 "**下一步**"。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-671">In the **Network Mix** page, click **Next**.</span></span>

    <span data-ttu-id="9b3b3-672">![在网络组合页面中单击 "下一步"](maintainable-azure-websites-managing-change-and-scale/_static/image94.png "在网络组合页面中单击 "下一步"")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-672">![Clicking next in the Network Mix page](maintainable-azure-websites-managing-change-and-scale/_static/image94.png "Clicking next in the Network Mix page")</span></span>

    <span data-ttu-id="9b3b3-673">*在网络组合页面中单击 "下一步"*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-673">*Clicking next in the Network Mix page*</span></span>
17. <span data-ttu-id="9b3b3-674">在 "**浏览器组合**" 页面中，选择**Internet Explorer 10.0**作为浏览器类型，然后单击 "**下一步**"。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-674">In the **Browser Mix** page, select **Internet Explorer 10.0** as the browser type and click **Next**.</span></span>

    <span data-ttu-id="9b3b3-675">![选择浏览器类型](maintainable-azure-websites-managing-change-and-scale/_static/image95.png "选择浏览器类型")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-675">![Selecting the browser type](maintainable-azure-websites-managing-change-and-scale/_static/image95.png "Selecting the browser type")</span></span>

    <span data-ttu-id="9b3b3-676">*选择浏览器类型*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-676">*Selecting the browser type*</span></span>
18. <span data-ttu-id="9b3b3-677">在 "**计数器集**" 页中，单击 "**下一步**"。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-677">In the **Counter Sets** page, click **Next**.</span></span>

    <span data-ttu-id="9b3b3-678">![在 "计数器集" 页中单击 "下一步"](maintainable-azure-websites-managing-change-and-scale/_static/image96.png "在 "计数器集" 页中单击 "下一步"")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-678">![Clicking Next in the Counter Sets page](maintainable-azure-websites-managing-change-and-scale/_static/image96.png "Clicking Next in the Counter Sets page")</span></span>

    <span data-ttu-id="9b3b3-679">*在 "计数器集" 页中单击 "下一步"*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-679">*Clicking Next in the Counter Sets page*</span></span>
19. <span data-ttu-id="9b3b3-680">在 "**运行设置**" 页中，将 "**负载测试持续时间**" 设置为**5 分钟**，然后单击 "**完成**"。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-680">In the **Run Settings** page, set the **Load test duration** to **5 minutes** and click **Finish**.</span></span>

    <span data-ttu-id="9b3b3-681">![将负载测试持续时间设置为5分钟](maintainable-azure-websites-managing-change-and-scale/_static/image97.png "将负载测试持续时间设置为5分钟")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-681">![Setting the load test duration to 5 minutes](maintainable-azure-websites-managing-change-and-scale/_static/image97.png "Setting the load test duration to 5 minutes")</span></span>

    <span data-ttu-id="9b3b3-682">*将负载测试持续时间设置为5分钟*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-682">*Setting the load test duration to 5 minutes*</span></span>
20. <span data-ttu-id="9b3b3-683">在**解决方案资源管理器**中，双击**本地设置**文件以浏览测试设置。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-683">In **Solution Explorer**, double-click the **Local.settings** file to explore the test settings.</span></span> <span data-ttu-id="9b3b3-684">默认情况下，Visual Studio 使用本地计算机来运行测试。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-684">By default, Visual Studio uses your local computer to run the tests.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9b3b3-685">或者，可以使用**Azure Test Plans**将测试项目配置为在云中运行负载测试。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-685">Alternatively, you can configure your test project to run the load tests in the cloud using **Azure Test Plans**.</span></span> <span data-ttu-id="9b3b3-686">Azure Test Plans 提供了一种基于云的负载测试服务，用于模拟更真实的负载，从而避免了本地环境约束（如 CPU 容量、可用内存和网络带宽）。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-686">Azure Test Plans provides a cloud-based load testing service that simulates a more realistic load, avoiding local environment constraints like CPU capacity, available memory, and network bandwidth.</span></span> <span data-ttu-id="9b3b3-687">有关使用 Azure Test Plans 运行负载测试的详细信息，请参阅[负载测试方案](/azure/devops/test/load-test/overview?view=vsts)。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-687">For more information about using Azure Test Plans to run load tests, see [Load testing scenarios](/azure/devops/test/load-test/overview?view=vsts).</span></span>

    ![测试设置](maintainable-azure-websites-managing-change-and-scale/_static/image98.png)

<a id="Ex5Task3"></a>
#### <a name="task-3--autoscale-verification"></a><span data-ttu-id="9b3b3-689">任务3–自动缩放验证</span><span class="sxs-lookup"><span data-stu-id="9b3b3-689">Task 3 – Autoscale Verification</span></span>

<span data-ttu-id="9b3b3-690">现在，你将执行在上一任务中创建的负载测试，并查看你的 web 应用在负载下的行为。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-690">You will now execute the load test you created in the previous task and see how your web app behaves under load.</span></span>

1. <span data-ttu-id="9b3b3-691">在**解决方案资源管理器**中，双击 " **LoadTest1** " 以打开负载测试。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-691">In **Solution Explorer**, double-click **LoadTest1.loadtest** to open the load test.</span></span>

    <span data-ttu-id="9b3b3-692">![打开 LoadTest1. loadtest](maintainable-azure-websites-managing-change-and-scale/_static/image99.png "打开 LoadTest1. loadtest")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-692">![Opening LoadTest1.loadtest](maintainable-azure-websites-managing-change-and-scale/_static/image99.png "Opening LoadTest1.loadtest")</span></span>

    <span data-ttu-id="9b3b3-693">*打开 LoadTest1. loadtest*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-693">*Opening LoadTest1.loadtest*</span></span>
2. <span data-ttu-id="9b3b3-694">在**LoadTest1 loadtest**窗口中，单击 "工具箱" 中的第一个按钮以运行负载测试。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-694">In the **LoadTest1.loadtest** window, click the first button in the toolbox to run the load test.</span></span>

    <span data-ttu-id="9b3b3-695">![运行负载测试](maintainable-azure-websites-managing-change-and-scale/_static/image100.png "运行负载测试")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-695">![Running the load test](maintainable-azure-websites-managing-change-and-scale/_static/image100.png "Running the load test")</span></span>

    <span data-ttu-id="9b3b3-696">*运行负载测试*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-696">*Running the load test*</span></span>
3. <span data-ttu-id="9b3b3-697">等待负载测试完成。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-697">Wait until the load test completes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9b3b3-698">负载测试模拟将请求同时发送到 web 应用的多个用户。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-698">The load test simulates multiple users that send requests to the web app simultaneously.</span></span> <span data-ttu-id="9b3b3-699">当测试正在运行时，您可以监视可用的计数器，以检测任何与您的负载测试运行有关的错误、警告或其他信息。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-699">When the test is running, you can monitor the available counters to detect any errors, warnings or other information related to your load test run.</span></span>

    <span data-ttu-id="9b3b3-700">![负载测试正在运行](maintainable-azure-websites-managing-change-and-scale/_static/image101.png "正在等待负载测试完成")</span><span class="sxs-lookup"><span data-stu-id="9b3b3-700">![Load test running](maintainable-azure-websites-managing-change-and-scale/_static/image101.png "Waiting until the load test completes")</span></span>

    <span data-ttu-id="9b3b3-701">*负载测试正在运行*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-701">*Load test running*</span></span>
4. <span data-ttu-id="9b3b3-702">测试完成后，返回到管理门户并导航到 web 应用的 "**缩放**" 页。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-702">Once the test completes, go back to the management portal and navigate to the **Scale** page of your web app.</span></span> <span data-ttu-id="9b3b3-703">在 "**容量**" 部分下，你应在图形中看到自动部署了新实例的。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-703">Under the **capacity** section, you should see in the graph that a new instance was automatically deployed.</span></span>

    ![已自动部署新实例](maintainable-azure-websites-managing-change-and-scale/_static/image102.png)

    <span data-ttu-id="9b3b3-705">*已自动部署新实例*</span><span class="sxs-lookup"><span data-stu-id="9b3b3-705">*New instance automatically deployed*</span></span>

    > [!NOTE]
    > <span data-ttu-id="9b3b3-706">可能需要花费几分钟时间，更改才会显示在图形中（定期按**CTRL + F5**刷新页面）。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-706">It may take several minutes for the changes to appear in the graph (press **CTRL + F5** periodically to refresh the page).</span></span> <span data-ttu-id="9b3b3-707">如果看不到任何更改，可以尝试以下操作：</span><span class="sxs-lookup"><span data-stu-id="9b3b3-707">If you do not see any changes, you can try the following:</span></span>
    >
    > - <span data-ttu-id="9b3b3-708">增加负载测试的持续时间（例如**10 分钟**）</span><span class="sxs-lookup"><span data-stu-id="9b3b3-708">Increase the duration of the load test (e.g. to **10 minutes**)</span></span>
    > - <span data-ttu-id="9b3b3-709">减少 web 应用的自动缩放配置中**目标 CPU**范围的最大值和最小值</span><span class="sxs-lookup"><span data-stu-id="9b3b3-709">Reduce the maximum and minimum values of the **Target CPU** range in the Autoscale configuration of your web app</span></span>
    > - <span data-ttu-id="9b3b3-710">在云中运行负载测试，并**Azure Test Plans**。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-710">Run the load test in the cloud with **Azure Test Plans**.</span></span> <span data-ttu-id="9b3b3-711">详细信息请参见[此处](/azure/devops/test/load-test/index?view=vsts)</span><span class="sxs-lookup"><span data-stu-id="9b3b3-711">More information [here](/azure/devops/test/load-test/index?view=vsts)</span></span>

---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="9b3b3-712">摘要</span><span class="sxs-lookup"><span data-stu-id="9b3b3-712">Summary</span></span>

<span data-ttu-id="9b3b3-713">在此动手实验中，你已了解如何在 Azure 中设置应用程序并将其部署到生产 web 应用。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-713">In this hands-on lab, you learned how to set up and deploy your application to production web apps in Azure.</span></span> <span data-ttu-id="9b3b3-714">首先，通过使用**Entity Framework Code First 迁移**检测和更新数据库，然后使用**Git**部署站点的新版本并执行回滚到最新稳定版本的站点。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-714">You started by detecting and updating your databases using **Entity Framework Code First Migrations**, then continued by deploying new versions of your site using **Git** and performing rollbacks to the latest stable version of your site.</span></span> <span data-ttu-id="9b3b3-715">此外，还了解了如何使用存储缩放应用，将静态内容移动到 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="9b3b3-715">Additionally, you learned how to scale your app using Storage to move your static content to a Blob container.</span></span>
