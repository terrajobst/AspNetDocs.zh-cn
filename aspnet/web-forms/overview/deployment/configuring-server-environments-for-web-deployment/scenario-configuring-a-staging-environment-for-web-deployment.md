---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-staging-environment-for-web-deployment
title: 方案：配置用于 Web 部署的过渡环境 |Microsoft Docs
author: jrjlee
description: 本主题介绍了过渡环境的典型 web 部署方案，并说明了设置类似环境所需完成的任务 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 5a8e49b7-5317-4125-b107-7e2466b47bb3
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-staging-environment-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: eaa61ca850817f8dd98955b59e94be93389bf256
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518006"
---
# <a name="scenario-configuring-a-staging-environment-for-web-deployment"></a><span data-ttu-id="eee07-103">方案：配置用于 Web 部署的过渡环境</span><span class="sxs-lookup"><span data-stu-id="eee07-103">Scenario: Configuring a Staging Environment for Web Deployment</span></span>

<span data-ttu-id="eee07-104">作者： [Jason](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="eee07-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="eee07-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="eee07-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="eee07-106">本主题介绍了过渡环境的典型 web 部署方案，并说明了设置类似环境需要完成的任务。</span><span class="sxs-lookup"><span data-stu-id="eee07-106">This topic describes a typical web deployment scenario for a staging environment and explains the tasks you need to complete in order to set up a similar environment.</span></span>

<span data-ttu-id="eee07-107">许多组织使用过渡环境预览 web 应用程序或网站的更新。</span><span class="sxs-lookup"><span data-stu-id="eee07-107">Lots of organizations use staging environments to preview updates to web applications or websites.</span></span> <span data-ttu-id="eee07-108">这样，组织中的人员就有机会在站点 "上线" 之前浏览和查看新功能或内容，或者将其部署到生产环境。</span><span class="sxs-lookup"><span data-stu-id="eee07-108">This gives people within the organization a chance to explore and review new functionality or content before the site "goes live," or in other words is deployed to a production environment.</span></span> <span data-ttu-id="eee07-109">过渡环境旨在尽可能密切地复制生产环境，以便提供逼真的预览。</span><span class="sxs-lookup"><span data-stu-id="eee07-109">The staging environment is designed to replicate the production environment as closely as possible, in order to provide a realistic preview.</span></span> <span data-ttu-id="eee07-110">这种类型的过渡环境通常具有以下特征：</span><span class="sxs-lookup"><span data-stu-id="eee07-110">This kind of staging environment typically has these characteristics:</span></span>

- <span data-ttu-id="eee07-111">环境包含多个负载均衡的 web 服务器和一个或多个数据库服务器，通常具有故障转移群集和数据库镜像。</span><span class="sxs-lookup"><span data-stu-id="eee07-111">The environment consists of multiple load-balanced web servers and one or more database servers, often with failover clustering and database mirroring.</span></span>
- <span data-ttu-id="eee07-112">应用程序可以由开发团队手动部署，也可以由团队生成服务器自动部署。</span><span class="sxs-lookup"><span data-stu-id="eee07-112">Applications may be deployed manually by a development team or automatically by a Team Build server.</span></span>
- <span data-ttu-id="eee07-113">部署应用程序的用户或进程帐户不太可能在临时服务器上具有管理员权限。</span><span class="sxs-lookup"><span data-stu-id="eee07-113">The users or process accounts that deploy applications are unlikely to have administrator privileges on the staging servers.</span></span>
- <span data-ttu-id="eee07-114">对应用程序的更改是频繁部署的，因此环境需要支持单步或自动部署。</span><span class="sxs-lookup"><span data-stu-id="eee07-114">Changes to applications are deployed on a frequent basis, so the environment needs to support single-step or automated deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="eee07-115">在多个服务器上横向扩展数据库部署超出了本教程的范围。</span><span class="sxs-lookup"><span data-stu-id="eee07-115">Scaling out a database deployment across multiple servers is beyond the scope of this tutorial.</span></span> <span data-ttu-id="eee07-116">有关此方面的详细信息，请参阅[SQL Server 联机丛书](https://technet.microsoft.com/library/ms130214.aspx)。</span><span class="sxs-lookup"><span data-stu-id="eee07-116">For more information on this area, please consult [SQL Server Books Online](https://technet.microsoft.com/library/ms130214.aspx).</span></span>

<span data-ttu-id="eee07-117">例如，在我们的 "[教程" 方案](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)中，TEAM FOUNDATION SERVER （TFS）管理 "联系人管理器" 解决方案。</span><span class="sxs-lookup"><span data-stu-id="eee07-117">For example, in our [tutorial scenario](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md), Team Foundation Server (TFS) manages the Contact Manager solution.</span></span> <span data-ttu-id="eee07-118">TFS 管理员 "Walters" 已创建生成定义，使开发人员可以根据需要触发到过渡环境的部署。</span><span class="sxs-lookup"><span data-stu-id="eee07-118">The TFS administrator, Rob Walters, has created a build definition that lets developers trigger a deployment to the staging environment as required.</span></span>

![](scenario-configuring-a-staging-environment-for-web-deployment/_static/image1.png)

<span data-ttu-id="eee07-119">请注意，在大多数情况下，不需要将最新版本部署到过渡环境。</span><span class="sxs-lookup"><span data-stu-id="eee07-119">Note that in most cases, you won't necessarily want to deploy the latest build to the staging environment.</span></span> <span data-ttu-id="eee07-120">相反，您很可能希望部署在测试环境中已经完成验证和验证的特定生成。</span><span class="sxs-lookup"><span data-stu-id="eee07-120">Instead, you're a lot more likely to want to deploy a specific build that has already undergone validation and verification in the test environment.</span></span>

## <a name="solution-overview"></a><span data-ttu-id="eee07-121">解决方案概述</span><span class="sxs-lookup"><span data-stu-id="eee07-121">Solution Overview</span></span>

<span data-ttu-id="eee07-122">在这种情况下，你可以通过分析部署要求来推导这些事实：</span><span class="sxs-lookup"><span data-stu-id="eee07-122">In this scenario, you can deduce these facts from an analysis of the deployment requirements:</span></span>

- <span data-ttu-id="eee07-123">执行部署的用户或进程帐户在过渡服务器上不具有管理员权限，因此过渡 web 服务器必须支持非管理员部署。</span><span class="sxs-lookup"><span data-stu-id="eee07-123">The user or process account that performs the deployment won't have administrator privileges on the staging servers, so the staging web servers must support non-administrator deployment.</span></span> <span data-ttu-id="eee07-124">因此，你需要将过渡 web 服务器配置为使用 Web 部署处理程序而不是远程代理。</span><span class="sxs-lookup"><span data-stu-id="eee07-124">As such, you'll need to configure the staging web servers to use the Web Deploy Handler rather than the remote agent.</span></span>
- <span data-ttu-id="eee07-125">过渡环境包含多个 web 服务器，但它需要支持一键式或自动部署，因此你需要使用 Web 场框架（WFF）来创建服务器场。</span><span class="sxs-lookup"><span data-stu-id="eee07-125">The staging environment includes multiple web servers, but it needs to support one-click or automated deployment, so you'll need to use the Web Farm Framework (WFF) to create a server farm.</span></span> <span data-ttu-id="eee07-126">使用此方法，你可以将应用程序部署到一台 web 服务器（主服务器），WFF 将在过渡环境中的所有其他 web 服务器上复制部署。</span><span class="sxs-lookup"><span data-stu-id="eee07-126">Using this approach, you can deploy an application to one web server (the primary server), and WFF will replicate the deployment on all the other web servers in the staging environment.</span></span>
- <span data-ttu-id="eee07-127">执行部署的用户或进程帐户必须具有创建数据库的权限。</span><span class="sxs-lookup"><span data-stu-id="eee07-127">The user or process account that performs the deployment must have permissions to create databases.</span></span> <span data-ttu-id="eee07-128">因此，除了配置数据库服务器以支持远程访问和部署之外，还需要将帐户添加到数据库服务器上的**dbcreator**服务器角色。</span><span class="sxs-lookup"><span data-stu-id="eee07-128">As such, you'll need to add the account to the **dbcreator** server role on the database server, in addition to configuring the database server to support remote access and deployment.</span></span>

<span data-ttu-id="eee07-129">以下主题提供完成这些任务所需的所有信息：</span><span class="sxs-lookup"><span data-stu-id="eee07-129">These topics provide all the information you need in order to complete these tasks:</span></span>

- <span data-ttu-id="eee07-130">[使用 Web 场框架创建服务器场](creating-a-server-farm-with-the-web-farm-framework.md)。</span><span class="sxs-lookup"><span data-stu-id="eee07-130">[Create a Server Farm with the Web Farm Framework](creating-a-server-farm-with-the-web-farm-framework.md).</span></span> <span data-ttu-id="eee07-131">本主题介绍如何使用 WFF 创建和配置服务器场，以便跨多个负载均衡的 web 服务器复制 web 平台产品和组件、配置设置以及网站和应用程序。</span><span class="sxs-lookup"><span data-stu-id="eee07-131">This topic describes how to create and configure a server farm using WFF, so that web platform products and components, configuration settings, and websites and applications are replicated across multiple load-balanced web servers.</span></span>
- <span data-ttu-id="eee07-132">[为 Web 部署发布（Web 部署处理程序）配置 Web 服务器](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)。</span><span class="sxs-lookup"><span data-stu-id="eee07-132">[Configure a Web Server for Web Deploy Publishing (Web Deploy Handler)](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md).</span></span> <span data-ttu-id="eee07-133">本主题介绍如何使用远程代理方法构建支持 Web 部署发布的 web 服务器，从干净的 Windows Server 2008 R2 版本开始。</span><span class="sxs-lookup"><span data-stu-id="eee07-133">This topic describes how to build a web server that supports Web Deploy publishing, using the remote agent approach, starting from a clean Windows Server 2008 R2 build.</span></span>
- <span data-ttu-id="eee07-134">[为 Web 部署发布配置数据库服务器](configuring-a-database-server-for-web-deploy-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="eee07-134">[Configure a Database Server for Web Deploy Publishing](configuring-a-database-server-for-web-deploy-publishing.md).</span></span> <span data-ttu-id="eee07-135">本主题介绍如何配置数据库服务器以支持远程访问和部署，从默认安装 SQL Server 2008 R2 开始。</span><span class="sxs-lookup"><span data-stu-id="eee07-135">This topic describes how to configure a database server to support remote access and deployment, starting from a default installation of SQL Server 2008 R2.</span></span>

## <a name="further-reading"></a><span data-ttu-id="eee07-136">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="eee07-136">Further Reading</span></span>

<span data-ttu-id="eee07-137">有关配置典型开发人员测试环境的指导，请参阅[方案：配置用于 Web 部署的测试环境](scenario-configuring-a-test-environment-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="eee07-137">For guidance on configuring a typical developer test environment, see [Scenario: Configuring a Test Environment for Web Deployment](scenario-configuring-a-test-environment-for-web-deployment.md).</span></span> <span data-ttu-id="eee07-138">有关配置典型生产环境的指南，请参阅[方案：配置用于 Web 部署的生产环境](scenario-configuring-a-production-environment-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="eee07-138">For guidance on configuring a typical production environment, see [Scenario: Configuring a Production Environment for Web Deployment](scenario-configuring-a-production-environment-for-web-deployment.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="eee07-139">[上一页](scenario-configuring-a-test-environment-for-web-deployment.md)
> [下一页](scenario-configuring-a-production-environment-for-web-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="eee07-139">[Previous](scenario-configuring-a-test-environment-for-web-deployment.md)
[Next](scenario-configuring-a-production-environment-for-web-deployment.md)</span></span>
