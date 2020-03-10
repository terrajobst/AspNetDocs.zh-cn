---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-test-environment-for-web-deployment
title: 方案：配置用于 Web 部署的测试环境 |Microsoft Docs
author: jrjlee
description: 本主题介绍了开发人员或测试环境的典型 web 部署方案，并说明了在设置 si 之前需要完成的任务。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 44a22ac7-1fc7-4174-b946-c6129fb6a19b
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-test-environment-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: d580e550f2461837f0e8a4e477273348b49cb53e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78517982"
---
# <a name="scenario-configuring-a-test-environment-for-web-deployment"></a><span data-ttu-id="f8039-103">方案：配置用于 Web 部署的测试环境</span><span class="sxs-lookup"><span data-stu-id="f8039-103">Scenario: Configuring a Test Environment for Web Deployment</span></span>

<span data-ttu-id="f8039-104">作者： [Jason](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="f8039-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="f8039-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="f8039-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="f8039-106">本主题介绍了开发人员或测试环境的典型 web 部署方案，并说明了设置类似环境需要完成的任务。</span><span class="sxs-lookup"><span data-stu-id="f8039-106">This topic describes a typical web deployment scenario for developer or test environments and explains the tasks you need to complete in order to set up a similar environment.</span></span>

<span data-ttu-id="f8039-107">当开发人员在 web 应用程序上工作时，他们通常会获得对服务器环境的访问权限，这些服务器环境可用于测试应用程序对应用程序所做的更改。</span><span class="sxs-lookup"><span data-stu-id="f8039-107">When developers work on web applications, they're often given access to a server environment that they can use to test changes to their applications in a realistic setting.</span></span> <span data-ttu-id="f8039-108">此类开发或测试环境通常具有以下特征：</span><span class="sxs-lookup"><span data-stu-id="f8039-108">This kind of development or test environment typically has these characteristics:</span></span>

- <span data-ttu-id="f8039-109">环境由单个 web 服务器和一个数据库服务器组成。</span><span class="sxs-lookup"><span data-stu-id="f8039-109">The environment consists of a single web server and a single database server.</span></span>
- <span data-ttu-id="f8039-110">开发人员通常在服务器上具有管理员权限，让他们将环境配置为应用程序的要求。</span><span class="sxs-lookup"><span data-stu-id="f8039-110">The developers usually have administrator privileges on the servers, to let them configure the environment to the requirements of their applications.</span></span>
- <span data-ttu-id="f8039-111">对应用程序的更改是频繁部署的，因此环境需要支持单步或自动部署。</span><span class="sxs-lookup"><span data-stu-id="f8039-111">Changes to applications are deployed on a frequent basis, so the environment needs to support single-step or automated deployment.</span></span>

<span data-ttu-id="f8039-112">例如，在我们的 "[教程" 方案](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)中，Matt Hink 是 Fabrikam，inc. 的开发人员正在处理 Contact Manager 解决方案，并且定期需要将更改部署到测试环境。</span><span class="sxs-lookup"><span data-stu-id="f8039-112">For example, in our [tutorial scenario](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md), Matt Hink is a developer at Fabrikam, Inc. Matt is working on the Contact Manager solution and regularly needs to deploy changes to a test environment.</span></span> <span data-ttu-id="f8039-113">Matt 是测试 web 服务器和测试数据库服务器上的管理员。</span><span class="sxs-lookup"><span data-stu-id="f8039-113">Matt is an administrator on the test web server and the test database server.</span></span> <span data-ttu-id="f8039-114">最初，Matt 需要能够直接将解决方案部署到测试环境。</span><span class="sxs-lookup"><span data-stu-id="f8039-114">Initially, Matt needs to be able to deploy the solution to the test environment directly.</span></span>

![](scenario-configuring-a-test-environment-for-web-deployment/_static/image1.png)

<span data-ttu-id="f8039-115">随着工作进度和更多开发人员加入团队，联系人管理器解决方案将配置为 Team Foundation Server （TFS）中的持续集成（CI）。</span><span class="sxs-lookup"><span data-stu-id="f8039-115">As work progresses and more developers join the team, the Contact Manager solution is configured for continuous integration (CI) in Team Foundation Server (TFS).</span></span> <span data-ttu-id="f8039-116">每当开发人员签入内容时，团队生成应生成解决方案，运行任何单元测试，并自动将解决方案部署到测试环境。</span><span class="sxs-lookup"><span data-stu-id="f8039-116">Whenever a developer checks in content, Team Build should build the solution, run any unit tests, and automatically deploy the solution to the test environment.</span></span>

![](scenario-configuring-a-test-environment-for-web-deployment/_static/image2.png)

## <a name="solution-overview"></a><span data-ttu-id="f8039-117">解决方案概述</span><span class="sxs-lookup"><span data-stu-id="f8039-117">Solution Overview</span></span>

<span data-ttu-id="f8039-118">测试环境需要支持远程计算机的单步或自动部署，因此你可以选择两种主要方法。</span><span class="sxs-lookup"><span data-stu-id="f8039-118">The test environment needs to support single-step or automated deployment from a remote computer, so you have a choice of two main approaches.</span></span> <span data-ttu-id="f8039-119">你可以：</span><span class="sxs-lookup"><span data-stu-id="f8039-119">You can:</span></span>

- <span data-ttu-id="f8039-120">使用 Web 部署代理服务配置测试 web 服务器以支持部署（"远程代理"）。</span><span class="sxs-lookup"><span data-stu-id="f8039-120">Configure the test web server to support deployment using the Web Deployment Agent Service (the "remote agent").</span></span>
- <span data-ttu-id="f8039-121">使用 Web 部署处理程序配置测试 web 服务器以支持部署。</span><span class="sxs-lookup"><span data-stu-id="f8039-121">Configure the test web server to support deployment using the Web Deploy handler.</span></span>

> [!NOTE]
> <span data-ttu-id="f8039-122">你还可以按[需使用 Web 部署](https://technet.microsoft.com/library/ee517345(WS.10).aspx)（"temp agent"）。</span><span class="sxs-lookup"><span data-stu-id="f8039-122">You could also use [Web Deploy On Demand](https://technet.microsoft.com/library/ee517345(WS.10).aspx) (the "temp agent").</span></span> <span data-ttu-id="f8039-123">这类似于要求和约束方面的远程代理方法。</span><span class="sxs-lookup"><span data-stu-id="f8039-123">This is similar to the remote agent approach in terms of requirements and constraints.</span></span>

<span data-ttu-id="f8039-124">在这种情况下，开发人员在目标服务器上具有管理员权限，而测试环境不受严格的安全约束的约束，因此，逻辑选择是将测试 web 服务器配置为支持使用远程代理进行的部署。</span><span class="sxs-lookup"><span data-stu-id="f8039-124">In this case, the developers have administrator privileges on the destination servers, and the test environment is not subject to strict security constraints, so the logical choice is to configure the test web server to support deployment using the remote agent.</span></span> <span data-ttu-id="f8039-125">这不太复杂，要求的初始配置比 Web 部署处理程序方法更少。</span><span class="sxs-lookup"><span data-stu-id="f8039-125">This is less complex and requires less initial configuration than the Web Deploy Handler approach.</span></span> <span data-ttu-id="f8039-126">还需要配置数据库服务器以支持远程访问和部署。</span><span class="sxs-lookup"><span data-stu-id="f8039-126">You'll also need to configure your database server to support remote access and deployment.</span></span>

<span data-ttu-id="f8039-127">以下主题提供完成这些任务所需的所有信息：</span><span class="sxs-lookup"><span data-stu-id="f8039-127">These topics provide all the information you need in order to complete these tasks:</span></span>

- <span data-ttu-id="f8039-128">[为 Web 部署发布（远程代理）配置 Web 服务器](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)。</span><span class="sxs-lookup"><span data-stu-id="f8039-128">[Configure a Web Server for Web Deploy Publishing (Remote Agent)](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md).</span></span> <span data-ttu-id="f8039-129">本主题介绍如何使用远程代理方法构建支持 Web 部署发布的 web 服务器，从干净的 Windows Server 2008 R2 版本开始。</span><span class="sxs-lookup"><span data-stu-id="f8039-129">This topic describes how to build a web server that supports Web Deploy publishing, using the remote agent approach, starting from a clean Windows Server 2008 R2 build.</span></span>
- <span data-ttu-id="f8039-130">[为 Web 部署发布配置数据库服务器](configuring-a-database-server-for-web-deploy-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="f8039-130">[Configure a Database Server for Web Deploy Publishing](configuring-a-database-server-for-web-deploy-publishing.md).</span></span> <span data-ttu-id="f8039-131">本主题介绍如何配置数据库服务器以支持远程访问和部署，从默认安装 SQL Server 2008 R2 开始。</span><span class="sxs-lookup"><span data-stu-id="f8039-131">This topic describes how to configure a database server to support remote access and deployment, starting from a default installation of SQL Server 2008 R2.</span></span>

## <a name="further-reading"></a><span data-ttu-id="f8039-132">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="f8039-132">Further Reading</span></span>

<span data-ttu-id="f8039-133">有关配置典型过渡环境的指导，请参阅[方案：配置用于 Web 部署的过渡环境](scenario-configuring-a-staging-environment-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="f8039-133">For guidance on configuring a typical staging environment, see [Scenario: Configuring a Staging Environment for Web Deployment](scenario-configuring-a-staging-environment-for-web-deployment.md).</span></span> <span data-ttu-id="f8039-134">有关配置典型生产环境的指南，请参阅[方案：配置用于 Web 部署的生产环境](scenario-configuring-a-production-environment-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="f8039-134">For guidance on configuring a typical production environment, see [Scenario: Configuring a Production Environment for Web Deployment](scenario-configuring-a-production-environment-for-web-deployment.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f8039-135">[上一页](choosing-the-right-approach-to-web-deployment.md)
> [下一页](scenario-configuring-a-staging-environment-for-web-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="f8039-135">[Previous](choosing-the-right-approach-to-web-deployment.md)
[Next](scenario-configuring-a-staging-environment-for-web-deployment.md)</span></span>
