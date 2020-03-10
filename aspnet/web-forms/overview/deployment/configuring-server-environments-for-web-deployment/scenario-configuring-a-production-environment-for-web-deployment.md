---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-production-environment-for-web-deployment
title: 方案：配置用于 Web 部署的生产环境 |Microsoft Docs
author: jrjlee
description: 本主题介绍了生产环境的典型 web 部署方案，并介绍了需要完成哪些任务才能设置类似 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 2e861511-450e-4752-a61e-4a01933f9b6e
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-production-environment-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 2d76e715cdbf6ec484fa0ff98b3b3d1d8dfd3961
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78515930"
---
# <a name="scenario-configuring-a-production-environment-for-web-deployment"></a><span data-ttu-id="73376-103">方案：配置用于 Web 部署的生产环境</span><span class="sxs-lookup"><span data-stu-id="73376-103">Scenario: Configuring a Production Environment for Web Deployment</span></span>

<span data-ttu-id="73376-104">作者： [Jason](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="73376-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="73376-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="73376-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="73376-106">本主题介绍了生产环境的典型 web 部署方案，并说明了设置类似环境需要完成的任务。</span><span class="sxs-lookup"><span data-stu-id="73376-106">This topic describes a typical web deployment scenario for a production environment and explains the tasks you need to complete in order to set up a similar environment.</span></span>

<span data-ttu-id="73376-107">生产环境是 web 应用程序或网站的最终目标。</span><span class="sxs-lookup"><span data-stu-id="73376-107">The production environment is the final destination for a web application or a website.</span></span> <span data-ttu-id="73376-108">至此，你的应用程序已通过测试，已部署到过渡环境，并已准备好 "上线"。</span><span class="sxs-lookup"><span data-stu-id="73376-108">By this point, your application has been through testing, has been deployed to a staging environment, and is ready to "go live."</span></span> <span data-ttu-id="73376-109">根据你的 web 内容的性质和用途、你的组织的规模、你的目标受众以及许多其他因素，生产环境的特征可能会有很大的差异。</span><span class="sxs-lookup"><span data-stu-id="73376-109">The characteristics of a production environment can vary widely according to the nature and purpose of your web content, the size of your organization, your target audience, and lots of other factors.</span></span> <span data-ttu-id="73376-110">在企业规模的方案中，生产环境可能具有以下特征：</span><span class="sxs-lookup"><span data-stu-id="73376-110">In an enterprise-scale scenario, the production environment may have these characteristics:</span></span>

- <span data-ttu-id="73376-111">环境包含多个负载均衡的 web 服务器和一个或多个数据库服务器，通常具有故障转移群集和数据库镜像。</span><span class="sxs-lookup"><span data-stu-id="73376-111">The environment consists of multiple load-balanced web servers and one or more database servers, often with failover clustering and database mirroring.</span></span>
- <span data-ttu-id="73376-112">如果环境面向 Internet，则很可能与内部网络隔离。</span><span class="sxs-lookup"><span data-stu-id="73376-112">If the environment is Internet-facing, it's likely to be segregated from your internal network.</span></span> <span data-ttu-id="73376-113">它可能位于外围网络中的不同子网中，它可能位于不同的域中，并且可能位于完全不同的网络基础结构上。</span><span class="sxs-lookup"><span data-stu-id="73376-113">It may be on a different subnet in a perimeter network, it may be on a different domain, and it may be on an entirely different network infrastructure.</span></span>
- <span data-ttu-id="73376-114">开发人员和生成服务器进程帐户在生产服务器上不太可能拥有管理员权限。</span><span class="sxs-lookup"><span data-stu-id="73376-114">Developers and build server process accounts are highly unlikely to have administrator privileges on the production servers.</span></span>
- <span data-ttu-id="73376-115">对应用程序所做的更改的部署频率低于测试或过渡部署。</span><span class="sxs-lookup"><span data-stu-id="73376-115">Changes to applications are deployed on a less frequent basis than test or staging deployments.</span></span>

> [!NOTE]
> <span data-ttu-id="73376-116">在多个服务器上横向扩展数据库部署超出了本教程的范围。</span><span class="sxs-lookup"><span data-stu-id="73376-116">Scaling out a database deployment across multiple servers is beyond the scope of this tutorial.</span></span> <span data-ttu-id="73376-117">有关此方面的详细信息，请参阅[SQL Server 联机丛书](https://technet.microsoft.com/library/ms130214.aspx)。</span><span class="sxs-lookup"><span data-stu-id="73376-117">For more information on this area, please consult [SQL Server Books Online](https://technet.microsoft.com/library/ms130214.aspx).</span></span>

<span data-ttu-id="73376-118">例如，在我们的[教程方案](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)中，团队生成服务器包含生成定义，使用户能够生成 Contact Manager 解决方案并在单个步骤中将其部署到过渡环境。</span><span class="sxs-lookup"><span data-stu-id="73376-118">For example, in our [tutorial scenario](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md), a Team Build server includes build definitions that let users build the Contact Manager solution and deploy it to a staging environment in a single step.</span></span> <span data-ttu-id="73376-119">当应用程序准备好部署到生产环境时，由于安全要求和网络基础结构施加的约束，生产环境管理员必须手动将 web 包复制到生产 web 服务器上并导入通过 Internet Information Services （IIS）管理器。</span><span class="sxs-lookup"><span data-stu-id="73376-119">When the application is ready to be deployed to production, due to the constraints imposed by security requirements and the network infrastructure, the production environment administrator must manually copy the web package onto a production web server and import it through Internet Information Services (IIS) Manager.</span></span>

![](scenario-configuring-a-production-environment-for-web-deployment/_static/image1.png)

## <a name="solution-overview"></a><span data-ttu-id="73376-120">解决方案概述</span><span class="sxs-lookup"><span data-stu-id="73376-120">Solution Overview</span></span>

<span data-ttu-id="73376-121">在这种情况下，你可以通过分析部署要求来推导这些事实：</span><span class="sxs-lookup"><span data-stu-id="73376-121">In this scenario, you can deduce these facts from an analysis of the deployment requirements:</span></span>

- <span data-ttu-id="73376-122">由于安全限制和网络配置，无法将生产环境配置为支持一键式或自动部署。</span><span class="sxs-lookup"><span data-stu-id="73376-122">Due to security restrictions and the network configuration, you can't configure the production environment to support one-click or automated deployment.</span></span> <span data-ttu-id="73376-123">脱机部署是此方案中唯一可行的方法。</span><span class="sxs-lookup"><span data-stu-id="73376-123">Offline deployment is the only viable approach in this scenario.</span></span>
- <span data-ttu-id="73376-124">生产环境包含多个 web 服务器，因此你可以使用 Web 场框架（WFF）来创建服务器场。</span><span class="sxs-lookup"><span data-stu-id="73376-124">The production environment includes multiple web servers, so you can use the Web Farm Framework (WFF) to create a server farm.</span></span> <span data-ttu-id="73376-125">使用此方法，管理员只需将该应用程序导入到一台 web 服务器（主服务器）上，WFF 将在生产环境中的所有其他 web 服务器上复制部署。</span><span class="sxs-lookup"><span data-stu-id="73376-125">Using this approach, the administrator only needs to import the application onto one web server (the primary server), and WFF will replicate the deployment on all the other web servers in the production environment.</span></span>

<span data-ttu-id="73376-126">以下主题提供完成这些任务所需的所有信息：</span><span class="sxs-lookup"><span data-stu-id="73376-126">These topics provide all the information you need in order to complete these tasks:</span></span>

- <span data-ttu-id="73376-127">[使用 Web 场框架创建服务器场](configuring-a-database-server-for-web-deploy-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="73376-127">[Create a Server Farm with the Web Farm Framework](configuring-a-database-server-for-web-deploy-publishing.md).</span></span> <span data-ttu-id="73376-128">本主题介绍如何使用 WFF 创建和配置服务器场，以便跨多个负载均衡的 web 服务器复制 web 平台产品和组件、配置设置以及网站和应用程序。</span><span class="sxs-lookup"><span data-stu-id="73376-128">This topic describes how to create and configure a server farm using WFF, so that web platform products and components, configuration settings, and websites and applications are replicated across multiple load-balanced web servers.</span></span>
- <span data-ttu-id="73376-129">[为 Web 部署发布（脱机部署）配置 Web 服务器](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="73376-129">[Configure a Web Server for Web Deploy Publishing (Offline Deployment)](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md).</span></span> <span data-ttu-id="73376-130">本主题介绍如何构建 web 服务器，使管理员能够从干净的 Windows Server 2008 R2 版本开始，手动导入和部署 web 包。</span><span class="sxs-lookup"><span data-stu-id="73376-130">This topic describes how to build a web server that lets administrators import and deploy web packages manually, starting from a clean Windows Server 2008 R2 build.</span></span>
- <span data-ttu-id="73376-131">[为 Web 部署发布配置数据库服务器](configuring-a-database-server-for-web-deploy-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="73376-131">[Configure a Database Server for Web Deploy Publishing](configuring-a-database-server-for-web-deploy-publishing.md).</span></span> <span data-ttu-id="73376-132">本主题介绍如何配置数据库服务器以支持远程访问和部署，从默认安装 SQL Server 2008 R2 开始。</span><span class="sxs-lookup"><span data-stu-id="73376-132">This topic describes how to configure a database server to support remote access and deployment, starting from a default installation of SQL Server 2008 R2.</span></span>

## <a name="further-reading"></a><span data-ttu-id="73376-133">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="73376-133">Further Reading</span></span>

<span data-ttu-id="73376-134">有关配置典型开发人员测试环境的指导，请参阅[方案：配置用于 Web 部署的测试环境](scenario-configuring-a-test-environment-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="73376-134">For guidance on configuring a typical developer test environment, see [Scenario: Configuring a Test Environment for Web Deployment](scenario-configuring-a-test-environment-for-web-deployment.md).</span></span> <span data-ttu-id="73376-135">有关配置典型过渡环境的指导，请参阅[方案：配置用于 Web 部署的过渡环境](scenario-configuring-a-staging-environment-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="73376-135">For guidance on configuring a typical staging environment, see [Scenario: Configuring a Staging Environment for Web Deployment](scenario-configuring-a-staging-environment-for-web-deployment.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="73376-136">[上一页](scenario-configuring-a-staging-environment-for-web-deployment.md)
> [下一页](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)</span><span class="sxs-lookup"><span data-stu-id="73376-136">[Previous](scenario-configuring-a-staging-environment-for-web-deployment.md)
[Next](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)</span></span>
