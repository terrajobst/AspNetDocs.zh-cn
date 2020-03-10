---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-permissions-for-team-build-deployment
title: 配置团队生成部署的权限 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何配置权限以使生成服务器能够将内容部署到 web 服务器和数据库服务器，作为自动 b 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 2488a91e-b0a8-465a-b874-3233f724b56b
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-permissions-for-team-build-deployment
msc.type: authoredcontent
ms.openlocfilehash: 5699f72af6b8d7f18d1a2c631dfdedd63c66e1e6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518504"
---
# <a name="configuring-permissions-for-team-build-deployment"></a><span data-ttu-id="a04e5-103">配置团队生成部署权限</span><span class="sxs-lookup"><span data-stu-id="a04e5-103">Configuring Permissions for Team Build Deployment</span></span>

<span data-ttu-id="a04e5-104">作者： [Jason](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="a04e5-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="a04e5-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="a04e5-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="a04e5-106">本主题介绍如何配置权限以使生成服务器能够将内容部署到 web 服务器和数据库服务器，作为自动生成过程的一部分。</span><span class="sxs-lookup"><span data-stu-id="a04e5-106">This topic describes how to configure permissions to enable your build server to deploy content to web servers and database servers as part of an automated build process.</span></span>

<span data-ttu-id="a04e5-107">本主题介绍一系列教程的一部分，这些教程基于名为 Fabrikam，Inc. 的虚构公司的企业部署要求。本教程系列使用一个示例解决方案&#x2014;，该解决方案使用[联系人管理器解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示具有真实复杂性级别的 web 应用程序，包括 ASP.NET MVC 3 应用程序、Windows Communication Foundation （WCF）服务和数据库项目。</span><span class="sxs-lookup"><span data-stu-id="a04e5-107">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="a04e5-108">这些教程核心的部署方法基于[理解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)中所述的拆分项目文件方法，其中，生成过程由两个项目文件&#x2014;控制，其中一个包含适用于每个目标环境的生成说明，另一个包含特定于环境的生成和部署设置。</span><span class="sxs-lookup"><span data-stu-id="a04e5-108">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="a04e5-109">在生成时，特定于环境的项目文件将合并到环境无关的项目文件中，以形成一组完整的生成说明。</span><span class="sxs-lookup"><span data-stu-id="a04e5-109">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="task-overview"></a><span data-ttu-id="a04e5-110">任务概述</span><span class="sxs-lookup"><span data-stu-id="a04e5-110">Task Overview</span></span>

<span data-ttu-id="a04e5-111">安装 Team Foundation Server （TFS）2010生成服务时，请指定要用于运行服务的标识。</span><span class="sxs-lookup"><span data-stu-id="a04e5-111">When you install the Team Foundation Server (TFS) 2010 build service, you specify the identity with which you want the service to run.</span></span> <span data-ttu-id="a04e5-112">默认情况下，这是 "网络服务" 帐户。</span><span class="sxs-lookup"><span data-stu-id="a04e5-112">By default, this is the Network Service account.</span></span> <span data-ttu-id="a04e5-113">或者，您可以将生成服务配置为使用域帐户运行。</span><span class="sxs-lookup"><span data-stu-id="a04e5-113">Alternatively, you can configure the build service to run using a domain account.</span></span>

<span data-ttu-id="a04e5-114">需要 Windows 身份验证的任何部署任务以及计划使用 Team Build 自动执行的部署任务将使用生成服务标识运行。</span><span class="sxs-lookup"><span data-stu-id="a04e5-114">Any deployment tasks that require Windows authentication, and that you plan to automate using Team Build, will run using the build service identity.</span></span> <span data-ttu-id="a04e5-115">因此，你需要向生成服务标识授予对 web 服务器和数据库服务器所需的任何权限。</span><span class="sxs-lookup"><span data-stu-id="a04e5-115">As such, you'll need to grant the build service identity any required permissions on your web servers and your database servers.</span></span>

> [!NOTE]
> <span data-ttu-id="a04e5-116">网络服务帐户使用计算机帐户向其他计算机进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="a04e5-116">The Network Service account uses the machine account to authenticate to other computers.</span></span> <span data-ttu-id="a04e5-117">计算机帐户采用 \* [域名] 格式\[计算机名称] \* **$** &#x2014;例如**FABRIKAM\TFSBUILD $** 。</span><span class="sxs-lookup"><span data-stu-id="a04e5-117">Machine accounts take the form \*[domain name]\[machine name]\***$**&#x2014;for example, **FABRIKAM\TFSBUILD$**.</span></span> <span data-ttu-id="a04e5-118">同样，如果你的生成服务使用网络服务标识运行，则应将任何所需的权限授予你的生成服务器的计算机帐户标识。</span><span class="sxs-lookup"><span data-stu-id="a04e5-118">As such, if your build service runs using the Network Service identity, you should grant any required permissions to the machine account identity for your build server.</span></span>

## <a name="configuring-web-server-permissions"></a><span data-ttu-id="a04e5-119">配置 Web 服务器权限</span><span class="sxs-lookup"><span data-stu-id="a04e5-119">Configuring Web Server Permissions</span></span>

<span data-ttu-id="a04e5-120">如[选择正确的 Web 部署方法](../configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment.md)中所述，如果要将 web 包部署到远程 web 服务器，可以使用以下两种主要方法：</span><span class="sxs-lookup"><span data-stu-id="a04e5-120">As described in [Choosing the Right Approach to Web Deployment](../configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment.md), there are two main approaches you can use if you want to deploy web packages to a remote web server:</span></span>

- <span data-ttu-id="a04e5-121">通过在目标服务器上以*Web 部署代理服务*（也称为远程代理）为目标来部署应用程序。</span><span class="sxs-lookup"><span data-stu-id="a04e5-121">Deploy the application from a remote location by targeting the *Web Deployment Agent Service* (also known as the remote agent) on the destination server.</span></span>
- <span data-ttu-id="a04e5-122">通过将目标服务器上的*Internet Information Services* （*IIS） Web 部署处理程序*作为目标来从远程位置部署应用程序。</span><span class="sxs-lookup"><span data-stu-id="a04e5-122">Deploy the application from a remote location by targeting the *Internet Information Services* (*IIS) Web Deploy Handler* on the destination server.</span></span>

<span data-ttu-id="a04e5-123">在这种情况下，远程代理有两个主要限制：</span><span class="sxs-lookup"><span data-stu-id="a04e5-123">The remote agent has two key limitations in this case:</span></span>

- <span data-ttu-id="a04e5-124">远程代理仅支持 NTLM 身份验证。</span><span class="sxs-lookup"><span data-stu-id="a04e5-124">The remote agent supports only NTLM authentication.</span></span> <span data-ttu-id="a04e5-125">换句话说，部署必须使用生成服务标识&#x2014;，而不能模拟其他帐户。</span><span class="sxs-lookup"><span data-stu-id="a04e5-125">In other words, the deployment must use the build service identity&#x2014;you can't impersonate another account.</span></span>
- <span data-ttu-id="a04e5-126">若要使用远程代理，执行部署的帐户必须是目标服务器上的管理员。</span><span class="sxs-lookup"><span data-stu-id="a04e5-126">To use the remote agent, the account that performs the deployment must be an administrator on the target server.</span></span>

<span data-ttu-id="a04e5-127">同时，这两种限制使得远程代理方法不适合自动团队生成部署。</span><span class="sxs-lookup"><span data-stu-id="a04e5-127">Together, these two limitations make the remote agent approach undesirable for an automated Team Build deployment.</span></span> <span data-ttu-id="a04e5-128">若要使用此方法，您需要使生成服务帐户成为任何目标 web 服务器上的管理员。</span><span class="sxs-lookup"><span data-stu-id="a04e5-128">To use this approach, you'd need to make the build service account an administrator on any target web servers.</span></span>

<span data-ttu-id="a04e5-129">与此相反，Web 部署处理程序方法具有以下优点：</span><span class="sxs-lookup"><span data-stu-id="a04e5-129">In contrast, the Web Deploy Handler approach offers various advantages:</span></span>

- <span data-ttu-id="a04e5-130">Web 部署处理程序支持通过 HTTPS 进行的基本身份验证，这允许你将备用帐户的凭据传递到 IIS Web 部署工具（Web 部署）。</span><span class="sxs-lookup"><span data-stu-id="a04e5-130">The Web Deploy Handler supports basic authentication over HTTPS, which allows you to pass the credentials of an alternative account to the IIS Web Deployment Tool (Web Deploy).</span></span>
- <span data-ttu-id="a04e5-131">你可以配置目标 web 服务器以允许非管理员用户使用 Web 部署处理程序将内容部署到特定的 IIS 网站。</span><span class="sxs-lookup"><span data-stu-id="a04e5-131">You can configure target web servers to allow non-administrator users to deploy content to specific IIS websites using the Web Deploy Handler.</span></span>

<span data-ttu-id="a04e5-132">因此，当你从 Team Build 自动部署 Web 包时，最好将 Web 部署处理程序设定为目标。</span><span class="sxs-lookup"><span data-stu-id="a04e5-132">As a result, it's clearly preferable to target the Web Deploy Handler when you automate web package deployment from Team Build.</span></span> <span data-ttu-id="a04e5-133">建议采用以下过程：</span><span class="sxs-lookup"><span data-stu-id="a04e5-133">This is the recommended process:</span></span>

1. <span data-ttu-id="a04e5-134">创建低特权域帐户以用于部署。</span><span class="sxs-lookup"><span data-stu-id="a04e5-134">Create a low-privileged domain account to use for the deployment.</span></span>
2. <span data-ttu-id="a04e5-135">配置 Web 部署处理程序，并向帐户授予向特定 IIS 网站部署内容所需的权限，如[配置用于 Web 部署发布的 Web 服务器（Web 部署处理程序）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="a04e5-135">Configure the Web Deploy Handler and grant the account the required permissions to deploy content to a specific IIS website, as described in [Configuring a Web Server for Web Deploy Publishing (Web Deploy Handler)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md).</span></span>
3. <span data-ttu-id="a04e5-136">调用 Web 部署，Web 部署并使用基本身份验证并提供所创建的域帐户的凭据，以执行部署。</span><span class="sxs-lookup"><span data-stu-id="a04e5-136">Invoke Web Deploy and target the Web Deploy Handler, using basic authentication and supplying the credentials of the domain account you created, to perform the deployment.</span></span>

<span data-ttu-id="a04e5-137">在 "[联系人管理器](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)" 示例解决方案中，您可以在特定于环境的项目文件中指定身份验证类型（基本或 NTLM）、Web 部署凭据和终结点地址（远程代理或 Web 部署处理程序）。</span><span class="sxs-lookup"><span data-stu-id="a04e5-137">In the [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) sample solution, you specify the authentication type (basic or NTLM), the Web Deploy credentials, and the endpoint address (remote agent or Web Deploy Handler) in the environment-specific project file.</span></span> <span data-ttu-id="a04e5-138">当执行项目文件时，这些值用于构建并运行 Web 部署命令。</span><span class="sxs-lookup"><span data-stu-id="a04e5-138">These values are used to formulate and run a Web Deploy command when the project file is executed.</span></span> <span data-ttu-id="a04e5-139">有关详细信息，请参阅[部署 Web 包](../web-deployment-in-the-enterprise/deploying-web-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="a04e5-139">For more information, see [Deploying Web Packages](../web-deployment-in-the-enterprise/deploying-web-packages.md).</span></span>

<span data-ttu-id="a04e5-140">有关配置 Web 部署处理程序的详细信息（包括如何配置权限），请参阅[配置 Web 服务器以进行 Web 部署发布（Web 部署处理程序）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)。</span><span class="sxs-lookup"><span data-stu-id="a04e5-140">For more information on configuring the Web Deploy Handler, including how to configure permissions, see [Configuring a Web Server for Web Deploy Publishing (Web Deploy Handler)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md).</span></span> <span data-ttu-id="a04e5-141">有关配置远程代理的详细信息，请参阅[为 Web 部署发布（远程代理）配置 Web 服务器](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)。</span><span class="sxs-lookup"><span data-stu-id="a04e5-141">For more information on configuring the remote agent, see [Configuring a Web Server for Web Deploy Publishing (Remote Agent)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent.md).</span></span>

## <a name="configuring-database-server-permissions"></a><span data-ttu-id="a04e5-142">配置数据库服务器权限</span><span class="sxs-lookup"><span data-stu-id="a04e5-142">Configuring Database Server Permissions</span></span>

<span data-ttu-id="a04e5-143">若要将数据库部署到 SQL Server，你必须：</span><span class="sxs-lookup"><span data-stu-id="a04e5-143">To deploy a database to SQL Server, you must:</span></span>

- <span data-ttu-id="a04e5-144">在 SQL Server 实例上创建部署帐户的登录名。</span><span class="sxs-lookup"><span data-stu-id="a04e5-144">Create a login for the deploying account on the SQL Server instance.</span></span>
- <span data-ttu-id="a04e5-145">向登录名授予对 SQL Server 实例的**DBCreator**权限。</span><span class="sxs-lookup"><span data-stu-id="a04e5-145">Grant the login **DBCreator** permissions on the SQL Server instance.</span></span>
- <span data-ttu-id="a04e5-146">初始部署后，将登录名添加到目标数据库的**db\_所有者**角色。</span><span class="sxs-lookup"><span data-stu-id="a04e5-146">After the initial deployment, add the login to the **db\_owner** role on the target database.</span></span> <span data-ttu-id="a04e5-147">这是必需的，因为在后续部署中，你要修改现有数据库，而不是创建新数据库。</span><span class="sxs-lookup"><span data-stu-id="a04e5-147">This is required because on subsequent deployments, you're modifying an existing database rather than creating a new database.</span></span>

<span data-ttu-id="a04e5-148">使用 NTLM 身份验证或 SQL Server 身份验证，可以对 SQL Server 实例进行身份验证：</span><span class="sxs-lookup"><span data-stu-id="a04e5-148">You can authenticate to a SQL Server instance using either NTLM authentication or SQL Server authentication:</span></span>

- <span data-ttu-id="a04e5-149">如果你使用 NTLM 身份验证，则需要向生成服务帐户授予上面所述的权限。</span><span class="sxs-lookup"><span data-stu-id="a04e5-149">If you use NTLM authentication, you need to grant the permissions described above to the build service account.</span></span>
- <span data-ttu-id="a04e5-150">如果使用 SQL Server 身份验证，则需要将上述权限授予 SQL Server 帐户。</span><span class="sxs-lookup"><span data-stu-id="a04e5-150">If you use SQL Server authentication, you need to grant the permissions described above to the SQL Server account.</span></span> <span data-ttu-id="a04e5-151">还需要在用于部署数据库的连接字符串中包含 SQL Server 用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="a04e5-151">You also need to include the SQL Server user name and password in the connection string you use to deploy the database.</span></span>

<span data-ttu-id="a04e5-152">有关如何配置数据库部署权限的分步详细信息，请参阅为[Web 部署发布配置数据库服务器](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="a04e5-152">For step-by-step details on how to configure permissions for database deployment, see [Configuring a Database Server for Web Deploy Publishing](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md).</span></span>

## <a name="conclusion"></a><span data-ttu-id="a04e5-153">结束语</span><span class="sxs-lookup"><span data-stu-id="a04e5-153">Conclusion</span></span>

<span data-ttu-id="a04e5-154">此时，你应该了解当你从 Team Build 自动执行 web 应用程序和数据库部署时，所需的权限以及为你打开的身份验证选项。</span><span class="sxs-lookup"><span data-stu-id="a04e5-154">At this point, you should understand the permissions required, together with the authentication options open to you, when you automate web application and database deployments from Team Build.</span></span> <span data-ttu-id="a04e5-155">还应能够在 IIS web 服务器和 SQL Server 数据库服务器上实现所需的权限。</span><span class="sxs-lookup"><span data-stu-id="a04e5-155">You should also be able to implement the necessary permissions on IIS web servers and SQL Server database servers.</span></span>

## <a name="further-reading"></a><span data-ttu-id="a04e5-156">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="a04e5-156">Further Reading</span></span>

<span data-ttu-id="a04e5-157">有关配置 Windows server 环境以支持远程部署的详细信息，请参阅[为 Web 部署配置服务器环境](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="a04e5-157">For more information on configuring Windows server environments to support remote deployment, see [Configuring Server Environments for Web Deployment](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="a04e5-158">上一页</span><span class="sxs-lookup"><span data-stu-id="a04e5-158">Previous</span></span>](deploying-a-specific-build.md)
