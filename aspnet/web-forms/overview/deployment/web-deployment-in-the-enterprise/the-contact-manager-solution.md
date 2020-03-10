---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/the-contact-manager-solution
title: Contact Manager 解决方案 |Microsoft Docs
author: jrjlee
description: 这一系列教程使用一个示例解决方案&#x2014;，该解决方案使用&#x2014;联系人管理器解决方案来表示企业规模的应用程序，该应用程序具有真实的上面 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 4d8c8d19-055b-4b70-9ee1-f748f0db3a01
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/the-contact-manager-solution
msc.type: authoredcontent
ms.openlocfilehash: 12ed7827f7392e559e04121386f7cd045de8462b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78473810"
---
# <a name="the-contact-manager-solution"></a><span data-ttu-id="f7bb9-103">Contact Manager 解决方案</span><span class="sxs-lookup"><span data-stu-id="f7bb9-103">The Contact Manager Solution</span></span>

<span data-ttu-id="f7bb9-104">作者： [Jason](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="f7bb9-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="f7bb9-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="f7bb9-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="f7bb9-106">这一[系列教程](web-deployment-in-the-enterprise.md)使用一个示例解决方案&#x2014;，其中使用了&#x2014;联系人管理器解决方案来表示企业规模的应用程序，该应用程序具有真实的复杂性级别。</span><span class="sxs-lookup"><span data-stu-id="f7bb9-106">This [series of tutorials](web-deployment-in-the-enterprise.md) uses a sample solution&#x2014;the Contact Manager solution&#x2014;to represent an enterprise-scale application with a realistic level of complexity.</span></span> <span data-ttu-id="f7bb9-107">本主题介绍联系人管理器解决方案，介绍解决方案的关键组件，并确定在企业环境中将此类应用程序部署到各种目标平台时面临的挑战。</span><span class="sxs-lookup"><span data-stu-id="f7bb9-107">This topic introduces the Contact Manager solution, describes the key components of the solution, and identifies the challenges in deploying this kind of application to various destination platforms in an enterprise environment.</span></span>
> 
> <span data-ttu-id="f7bb9-108">当你完成这些教程中的各个主题时，你可以使用 Contact Manager 解决方案作为参考实现，演示如何在企业部署方案中满足特定挑战。</span><span class="sxs-lookup"><span data-stu-id="f7bb9-108">As you work through the topics in these tutorials, you can use the Contact Manager solution as a reference implementation that demonstrates how you can meet specific challenges in enterprise deployment scenarios.</span></span> <span data-ttu-id="f7bb9-109">下一主题 "[设置联系人管理器" 解决方案](setting-up-the-contact-manager-solution.md)介绍了如何在开发人员工作站上下载和运行解决方案。</span><span class="sxs-lookup"><span data-stu-id="f7bb9-109">The next topic, [Setting Up the Contact Manager Solution](setting-up-the-contact-manager-solution.md), describes how to download and run the solution on your developer workstation.</span></span>

## <a name="solution-overview"></a><span data-ttu-id="f7bb9-110">解决方案概述</span><span class="sxs-lookup"><span data-stu-id="f7bb9-110">Solution Overview</span></span>

<span data-ttu-id="f7bb9-111">Contact Manager 解决方案由四个单独的项目组成：</span><span class="sxs-lookup"><span data-stu-id="f7bb9-111">The Contact Manager solution consists of four individual projects:</span></span>

![](the-contact-manager-solution/_static/image1.png)

- <span data-ttu-id="f7bb9-112">**ContactManager**。</span><span class="sxs-lookup"><span data-stu-id="f7bb9-112">**ContactManager.Mvc**.</span></span> <span data-ttu-id="f7bb9-113">这是一个 ASP.NET MVC 3 web 应用程序项目，它表示解决方案的入口点。</span><span class="sxs-lookup"><span data-stu-id="f7bb9-113">This is an ASP.NET MVC 3 web application project that represents the entry point for the solution.</span></span> <span data-ttu-id="f7bb9-114">它提供了一些基本 web 应用程序功能，例如，为用户提供创建和查看联系人详细信息的能力。</span><span class="sxs-lookup"><span data-stu-id="f7bb9-114">It offers some basic web application functionality, like providing users with the ability to create and view contact details.</span></span> <span data-ttu-id="f7bb9-115">应用程序依赖于 Windows Communication Foundation （WCF）服务来管理联系人，并使用 ASP.NET 应用程序服务数据库来管理身份验证和授权。</span><span class="sxs-lookup"><span data-stu-id="f7bb9-115">The application relies on a Windows Communication Foundation (WCF) service to manage contacts and an ASP.NET application services database to manage authentication and authorization.</span></span>
- <span data-ttu-id="f7bb9-116">**ContactManager**。</span><span class="sxs-lookup"><span data-stu-id="f7bb9-116">**ContactManager.Database**.</span></span> <span data-ttu-id="f7bb9-117">这是一个 Visual Studio 数据库项目。</span><span class="sxs-lookup"><span data-stu-id="f7bb9-117">This is a Visual Studio database project.</span></span> <span data-ttu-id="f7bb9-118">项目定义用于存储联系人详细信息的数据库的架构。</span><span class="sxs-lookup"><span data-stu-id="f7bb9-118">The project defines the schema for a database that stores contact details.</span></span>
- <span data-ttu-id="f7bb9-119">**ContactManager**。</span><span class="sxs-lookup"><span data-stu-id="f7bb9-119">**ContactManager.Service**.</span></span> <span data-ttu-id="f7bb9-120">这是一个 WCF web services 项目。</span><span class="sxs-lookup"><span data-stu-id="f7bb9-120">This is a WCF web service project.</span></span> <span data-ttu-id="f7bb9-121">WCF 服务公开一个终结点，该终结点允许调用方对**ContactManager**数据库执行创建、检索、更新和删除（CRUD）操作。</span><span class="sxs-lookup"><span data-stu-id="f7bb9-121">The WCF service exposes an endpoint that allows callers to perform create, retrieve, update, and delete (CRUD) operations on the **ContactManager** database.</span></span> <span data-ttu-id="f7bb9-122">该服务依赖于**ContactManager**数据库和**ContactManager**程序集。</span><span class="sxs-lookup"><span data-stu-id="f7bb9-122">The service relies on the **ContactManager** database and the **ContactManager.Common.dll** assembly.</span></span>
- <span data-ttu-id="f7bb9-123">**ContactManager**。</span><span class="sxs-lookup"><span data-stu-id="f7bb9-123">**ContactManager.Common**.</span></span> <span data-ttu-id="f7bb9-124">这是一个类库项目。</span><span class="sxs-lookup"><span data-stu-id="f7bb9-124">This is a class library project.</span></span> <span data-ttu-id="f7bb9-125">WCF 服务依赖于此程序集中定义的类型。</span><span class="sxs-lookup"><span data-stu-id="f7bb9-125">The WCF service relies on types defined in this assembly.</span></span>

<span data-ttu-id="f7bb9-126">此解决方案还包括一个名为 Publish 的解决方案文件夹。</span><span class="sxs-lookup"><span data-stu-id="f7bb9-126">The solution also includes a solution folder named Publish.</span></span> <span data-ttu-id="f7bb9-127">其中包含各种自定义项目文件和命令文件，它们演示了如何控制和操作生成和部署过程。</span><span class="sxs-lookup"><span data-stu-id="f7bb9-127">This contains various custom project files and command files that demonstrate how you can control and manipulate the build and deployment process.</span></span> <span data-ttu-id="f7bb9-128">本教程稍后将对这些内容进行更详细的介绍。</span><span class="sxs-lookup"><span data-stu-id="f7bb9-128">These are covered in more detail later in this tutorial.</span></span>

<span data-ttu-id="f7bb9-129">在概念级别上，解决方案的组件组合在一起，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f7bb9-129">At a conceptual level, the components of the solution fit together like this:</span></span>

![](the-contact-manager-solution/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="f7bb9-130">尽管 ASP.NET MVC 3 web 应用程序使用 ASP.NET 成员资格提供程序，但 web 应用程序中的所有页面都允许匿名访问。</span><span class="sxs-lookup"><span data-stu-id="f7bb9-130">While the ASP.NET MVC 3 web application uses the ASP.NET membership provider, all the pages within the web application allow anonymous access.</span></span> <span data-ttu-id="f7bb9-131">这显然不是真实的配置。</span><span class="sxs-lookup"><span data-stu-id="f7bb9-131">This is clearly not a realistic configuration.</span></span> <span data-ttu-id="f7bb9-132">不过，解决方案是以这种方式设置的，使你可以更轻松地部署和测试解决方案，而无需配置用户帐户和角色。</span><span class="sxs-lookup"><span data-stu-id="f7bb9-132">However, the solution is set up in this way to make it easier for you to deploy and test the solution without configuring user accounts and roles.</span></span>

## <a name="deployment-challenges"></a><span data-ttu-id="f7bb9-133">部署难题</span><span class="sxs-lookup"><span data-stu-id="f7bb9-133">Deployment Challenges</span></span>

<span data-ttu-id="f7bb9-134">"联系人管理器" 解决方案阐明了许多企业部署方案中常见的一些部署难题：</span><span class="sxs-lookup"><span data-stu-id="f7bb9-134">The Contact Manager solution illustrates several deployment challenges that are common to lots of enterprise deployment scenarios:</span></span>

- <span data-ttu-id="f7bb9-135">解决方案包含多个依赖项目。</span><span class="sxs-lookup"><span data-stu-id="f7bb9-135">The solution consists of multiple dependent projects.</span></span> <span data-ttu-id="f7bb9-136">你需要同时部署这些项目。</span><span class="sxs-lookup"><span data-stu-id="f7bb9-136">You need to deploy these projects simultaneously.</span></span>
- <span data-ttu-id="f7bb9-137">需要为每个环境更新连接字符串和服务终结点，在很多情况下，这些信息将不能供开发人员使用。</span><span class="sxs-lookup"><span data-stu-id="f7bb9-137">Connection strings and service endpoints need to be updated for each environment, and in a lot of cases this information will not be available to the developer.</span></span>
- <span data-ttu-id="f7bb9-138">将**ContactManager**数据库部署到过渡环境和生产环境时，需要在后续部署中保留现有数据。</span><span class="sxs-lookup"><span data-stu-id="f7bb9-138">When you deploy the **ContactManager** database to staging and production environments, you need to preserve existing data on subsequent deployments.</span></span>
- <span data-ttu-id="f7bb9-139">部署 ASP.NET 应用程序服务数据库时，需要部署某些配置数据，但要省略任何用户帐户数据。</span><span class="sxs-lookup"><span data-stu-id="f7bb9-139">When you deploy the ASP.NET application services database, you need to deploy some configuration data but omit any user account data.</span></span>
- <span data-ttu-id="f7bb9-140">这些项目包括一些不应部署的文件和文件夹。</span><span class="sxs-lookup"><span data-stu-id="f7bb9-140">The projects include some files and folders that should not be deployed.</span></span> <span data-ttu-id="f7bb9-141">需要从部署过程中排除这些文件和文件夹。</span><span class="sxs-lookup"><span data-stu-id="f7bb9-141">You need to exclude these files and folders from the deployment process.</span></span>
- <span data-ttu-id="f7bb9-142">解决方案需要支持从 Team Foundation Server （TFS）生成服务器自动部署。</span><span class="sxs-lookup"><span data-stu-id="f7bb9-142">The solution needs to support automated deployment from a Team Foundation Server (TFS) build server.</span></span>

## <a name="conclusion"></a><span data-ttu-id="f7bb9-143">结束语</span><span class="sxs-lookup"><span data-stu-id="f7bb9-143">Conclusion</span></span>

<span data-ttu-id="f7bb9-144">本主题提供了联系人管理器解决方案的高级概述，并确定了许多企业部署方案中常见的一些固有的部署挑战。</span><span class="sxs-lookup"><span data-stu-id="f7bb9-144">This topic provided a high-level overview of the Contact Manager solution and identified some of the inherent deployment challenges that are common to lots of enterprise deployment scenarios.</span></span> <span data-ttu-id="f7bb9-145">本教程中的其余主题介绍了可用于解决这些难题的一些方法。</span><span class="sxs-lookup"><span data-stu-id="f7bb9-145">The remaining topics in this tutorial describe some of the techniques you can use to meet these challenges.</span></span>

<span data-ttu-id="f7bb9-146">下一主题 "[设置联系人管理器" 解决方案](setting-up-the-contact-manager-solution.md)介绍了如何在开发人员工作站上下载和运行解决方案。</span><span class="sxs-lookup"><span data-stu-id="f7bb9-146">The next topic, [Setting Up the Contact Manager Solution](setting-up-the-contact-manager-solution.md), describes how to download and run the solution on your developer workstation.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f7bb9-147">[上一页](web-deployment-in-the-enterprise.md)
> [下一页](setting-up-the-contact-manager-solution.md)</span><span class="sxs-lookup"><span data-stu-id="f7bb9-147">[Previous](web-deployment-in-the-enterprise.md)
[Next](setting-up-the-contact-manager-solution.md)</span></span>
