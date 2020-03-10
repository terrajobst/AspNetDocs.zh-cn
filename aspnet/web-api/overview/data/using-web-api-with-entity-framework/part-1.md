---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-1
title: 将 Web API 2 与实体框架6一起使用 |Microsoft Docs
author: MikeWasson
description: 本教程将教你使用 ASP.NET Web API 后端创建 web 应用程序的基础知识。 本教程使用实体框架6作为数据布局 。
ms.author: riande
ms.date: 01/17/2019
ms.assetid: e879487e-dbcd-4b33-b092-d67c37ae768c
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-1
msc.type: authoredcontent
ms.openlocfilehash: 0f5dc960f494af5bd4ce87863a510d1892319908
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504836"
---
# <a name="using-web-api-2-with-entity-framework-6"></a><span data-ttu-id="3eb8f-104">通过 Entity Framework 6 使用 Web API 2</span><span class="sxs-lookup"><span data-stu-id="3eb8f-104">Using Web API 2 with Entity Framework 6</span></span>

[<span data-ttu-id="3eb8f-105">下载完成的项目</span><span class="sxs-lookup"><span data-stu-id="3eb8f-105">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

> <span data-ttu-id="3eb8f-106">本教程介绍使用 ASP.NET Web API 后端创建 web 应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="3eb8f-106">This tutorial teaches you the basics of creating a web application with an ASP.NET Web API back end.</span></span> <span data-ttu-id="3eb8f-107">本教程将实体框架6用于数据层，并为客户端 JavaScript 应用程序使用 "挖空"。</span><span class="sxs-lookup"><span data-stu-id="3eb8f-107">The tutorial uses Entity Framework 6 for the data layer, and Knockout.js for the client-side JavaScript application.</span></span> <span data-ttu-id="3eb8f-108">本教程还演示了如何将应用部署到 Azure App Service Web Apps。</span><span class="sxs-lookup"><span data-stu-id="3eb8f-108">The tutorial also shows how to deploy the app to Azure App Service Web Apps.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="3eb8f-109">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="3eb8f-109">Software versions used in the tutorial</span></span>
>
> - <span data-ttu-id="3eb8f-110">Web API 2。1</span><span class="sxs-lookup"><span data-stu-id="3eb8f-110">Web API 2.1</span></span>
> - <span data-ttu-id="3eb8f-111">Visual Studio 2017 （下载 Visual Studio 2017[此处](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)）</span><span class="sxs-lookup"><span data-stu-id="3eb8f-111">Visual Studio 2017 (download Visual Studio 2017 [here](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))</span></span>
> - <span data-ttu-id="3eb8f-112">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="3eb8f-112">Entity Framework 6</span></span>
> - <span data-ttu-id="3eb8f-113">.NET 4.7</span><span class="sxs-lookup"><span data-stu-id="3eb8f-113">.NET 4.7</span></span>
> - <span data-ttu-id="3eb8f-114">[挖空 .js](http://knockoutjs.com/) 3。1</span><span class="sxs-lookup"><span data-stu-id="3eb8f-114">[Knockout.js](http://knockoutjs.com/) 3.1</span></span>

<span data-ttu-id="3eb8f-115">本教程将 ASP.NET Web API 2 与实体框架6一起使用，以创建操作后端数据库的 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="3eb8f-115">This tutorial uses ASP.NET Web API 2 with Entity Framework 6 to create a web application that manipulates a back-end database.</span></span> <span data-ttu-id="3eb8f-116">下面是你将创建的应用程序的屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="3eb8f-116">Here is a screen shot of the application that you will create.</span></span>

[![](part-1/_static/image2.png)](part-1/_static/image1.png)

<span data-ttu-id="3eb8f-117">应用使用单页应用程序（SPA）设计。</span><span class="sxs-lookup"><span data-stu-id="3eb8f-117">The app uses a single-page application (SPA) design.</span></span> <span data-ttu-id="3eb8f-118">"单页应用程序" 是 web 应用程序的常规术语，用于加载单个 HTML 页面，然后动态更新页面，而不是加载新页面。</span><span class="sxs-lookup"><span data-stu-id="3eb8f-118">"Single-page application" is the general term for a web application that loads a single HTML page and then updates the page dynamically, instead of loading new pages.</span></span> <span data-ttu-id="3eb8f-119">初始页面加载后，应用将通过 AJAX 请求与服务器进行通信。</span><span class="sxs-lookup"><span data-stu-id="3eb8f-119">After the initial page load, the app talks with the server through AJAX requests.</span></span> <span data-ttu-id="3eb8f-120">AJAX 请求返回 JSON 数据，应用使用这些数据来更新 UI。</span><span class="sxs-lookup"><span data-stu-id="3eb8f-120">The AJAX requests return JSON data, which the app uses to update the UI.</span></span>

<span data-ttu-id="3eb8f-121">AJAX 并不新，但现在有了 JavaScript 框架，可以更轻松地构建和维护大型的 SPA 应用程序。</span><span class="sxs-lookup"><span data-stu-id="3eb8f-121">AJAX isn't new, but today there are JavaScript frameworks that make it easier to build and maintain a large sophisticated SPA application.</span></span> <span data-ttu-id="3eb8f-122">本教程使用的是[挖空](http://knockoutjs.com/)的，但你可以使用任何 JavaScript 客户端框架。</span><span class="sxs-lookup"><span data-stu-id="3eb8f-122">This tutorial uses [Knockout.js](http://knockoutjs.com/), but you can use any JavaScript client framework.</span></span>

<span data-ttu-id="3eb8f-123">下面是此应用程序的主要构建基块：</span><span class="sxs-lookup"><span data-stu-id="3eb8f-123">Here are the main building blocks for this app:</span></span>

- <span data-ttu-id="3eb8f-124">ASP.NET MVC 创建 HTML 页面。</span><span class="sxs-lookup"><span data-stu-id="3eb8f-124">ASP.NET MVC creates the HTML page.</span></span>
- <span data-ttu-id="3eb8f-125">ASP.NET Web API 处理 AJAX 请求并返回 JSON 数据。</span><span class="sxs-lookup"><span data-stu-id="3eb8f-125">ASP.NET Web API handles the AJAX requests and returns JSON data.</span></span>
- <span data-ttu-id="3eb8f-126">挖空 node.js 数据-将 HTML 元素绑定到 JSON 数据。</span><span class="sxs-lookup"><span data-stu-id="3eb8f-126">Knockout.js data-binds the HTML elements to the JSON data.</span></span>
- <span data-ttu-id="3eb8f-127">实体框架与数据库进行通信。</span><span class="sxs-lookup"><span data-stu-id="3eb8f-127">Entity Framework talks to the database.</span></span>

## <a name="see-this-app-running-on-azure"></a><span data-ttu-id="3eb8f-128">查看此应用在 Azure 上运行</span><span class="sxs-lookup"><span data-stu-id="3eb8f-128">See this app running on Azure</span></span>

<span data-ttu-id="3eb8f-129">要查看作为实时 web 应用运行的已完成站点吗？</span><span class="sxs-lookup"><span data-stu-id="3eb8f-129">Would you like to see the finished site running as a live web app?</span></span> <span data-ttu-id="3eb8f-130">可以通过选择以下按钮将应用程序的完整版本部署到 Azure 帐户。</span><span class="sxs-lookup"><span data-stu-id="3eb8f-130">You can deploy a complete version of the app to your Azure account by selecting the following button.</span></span>

[![](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/BookService)

<span data-ttu-id="3eb8f-131">需要一个 Azure 帐户才能将此解决方案部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="3eb8f-131">You need an Azure account to deploy this solution to Azure.</span></span> <span data-ttu-id="3eb8f-132">如果还没有帐户，可以使用以下选项：</span><span class="sxs-lookup"><span data-stu-id="3eb8f-132">If you do not already have an account, you have the following options:</span></span>

- <span data-ttu-id="3eb8f-133">[免费打开 Azure 帐户](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604)-获取可用来试用付费版 Azure 服务的信用额度，甚至在用完信用额度后，你仍可以保留帐户和使用免费的 azure 服务。</span><span class="sxs-lookup"><span data-stu-id="3eb8f-133">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="3eb8f-134">[激活 msdn 订户权益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)-msdn 订阅每月提供可用于付费 Azure 服务的信用额度。</span><span class="sxs-lookup"><span data-stu-id="3eb8f-134">[Activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

## <a name="create-the-project"></a><span data-ttu-id="3eb8f-135">创建项目</span><span class="sxs-lookup"><span data-stu-id="3eb8f-135">Create the project</span></span>

<span data-ttu-id="3eb8f-136">打开 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="3eb8f-136">Open Visual Studio.</span></span> <span data-ttu-id="3eb8f-137">从 "**文件**" 菜单中选择 "**新建**"，然后选择 "**项目**"。</span><span class="sxs-lookup"><span data-stu-id="3eb8f-137">From the **File** menu, select **New**, then select **Project**.</span></span> <span data-ttu-id="3eb8f-138">（或在 "开始" 页上选择 "**新建项目**"。）</span><span class="sxs-lookup"><span data-stu-id="3eb8f-138">(Or select **New Project** on the Start page.)</span></span>

<span data-ttu-id="3eb8f-139">在 "**新建项目**" 对话框中，在左窗格中选择 " **web** "，并在中间窗格中选择 " **ASP.NET web 应用程序（.NET Framework）** "。</span><span class="sxs-lookup"><span data-stu-id="3eb8f-139">In the **New Project** dialog, select **Web** in the left pane and **ASP.NET Web Application (.NET Framework)** in the middle pane.</span></span> <span data-ttu-id="3eb8f-140">将项目命名为**BookService** ，然后选择 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="3eb8f-140">Name the project **BookService** and select **OK**.</span></span>

[![](part-1/_static/image11.png)](part-1/_static/image11.png)

<span data-ttu-id="3eb8f-141">在 "**新建 ASP.NET 项目**" 对话框中，选择 " **Web API** " 模板。</span><span class="sxs-lookup"><span data-stu-id="3eb8f-141">In the **New ASP.NET Project** dialog, select the **Web API** template.</span></span>

[![](part-1/_static/image12.png)](part-1/_static/image12.png)

<span data-ttu-id="3eb8f-142">选择“确定”创建项目。</span><span class="sxs-lookup"><span data-stu-id="3eb8f-142">Select **OK** to create the project.</span></span>

## <a name="configure-azure-settings-optional"></a><span data-ttu-id="3eb8f-143">配置 Azure 设置（可选）</span><span class="sxs-lookup"><span data-stu-id="3eb8f-143">Configure Azure settings (optional)</span></span>

<span data-ttu-id="3eb8f-144">创建项目后，可以随时选择部署到 Azure App Service Web 应用。</span><span class="sxs-lookup"><span data-stu-id="3eb8f-144">After you create the project, you can choose to deploy to Azure App Service Web Apps at any time.</span></span> 

1. <span data-ttu-id="3eb8f-145">在解决方案资源管理器中，右键单击项目，然后选择 "**发布**"。</span><span class="sxs-lookup"><span data-stu-id="3eb8f-145">In Solution Explorer, right-click on your project and select **Publish**.</span></span>

2. <span data-ttu-id="3eb8f-146">在出现的窗口中，选择 "**启动**"。</span><span class="sxs-lookup"><span data-stu-id="3eb8f-146">In the window that appears, select **Start**.</span></span> <span data-ttu-id="3eb8f-147">此时将显示 "**选取发布目标**" 对话框。</span><span class="sxs-lookup"><span data-stu-id="3eb8f-147">The **Pick a publish target** dialog box appears.</span></span>

   [![](part-1/_static/image14.png)](part-1/_static/image14.png)

3. <span data-ttu-id="3eb8f-148">选择“创建配置文件”。</span><span class="sxs-lookup"><span data-stu-id="3eb8f-148">Select **Create Profile**.</span></span> <span data-ttu-id="3eb8f-149">“创建应用服务”对话框随即显示。</span><span class="sxs-lookup"><span data-stu-id="3eb8f-149">The **Create App Service** dialog box appears.</span></span>

   [![](part-1/_static/image15.png)](part-1/_static/image15.png)

   <span data-ttu-id="3eb8f-150">接受默认值，或者为应用程序名称、资源组、托管计划、Azure 订阅和地理区域输入不同的值。</span><span class="sxs-lookup"><span data-stu-id="3eb8f-150">Accept the defaults, or enter different values for the application name, resource group, hosting plan, Azure subscription, and geographical region.</span></span> 

4. <span data-ttu-id="3eb8f-151">选择 "**创建 SQL 数据库**"。</span><span class="sxs-lookup"><span data-stu-id="3eb8f-151">Select **Create a SQL database**.</span></span> <span data-ttu-id="3eb8f-152">此时将显示 "**配置 SQL Server** " 对话框。</span><span class="sxs-lookup"><span data-stu-id="3eb8f-152">The **Configure SQL Server** dialog box appears.</span></span> 

   [![](part-1/_static/image16.png)](part-1/_static/image16.png)

   <span data-ttu-id="3eb8f-153">接受默认值或输入不同的值。</span><span class="sxs-lookup"><span data-stu-id="3eb8f-153">Accept the defaults or enter different values.</span></span> <span data-ttu-id="3eb8f-154">输入新数据库的**管理员用户名**和**管理员密码**。</span><span class="sxs-lookup"><span data-stu-id="3eb8f-154">Enter an **Administrator Username** and **Administrator Password** for your new database.</span></span> <span data-ttu-id="3eb8f-155">完成后，选择 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="3eb8f-155">Select **OK** when you're done.</span></span> <span data-ttu-id="3eb8f-156">再次出现 "**创建应用服务**" 页。</span><span class="sxs-lookup"><span data-stu-id="3eb8f-156">The **Create App Service** page reappears.</span></span>

5. <span data-ttu-id="3eb8f-157">选择 "**创建**" 以创建配置文件。</span><span class="sxs-lookup"><span data-stu-id="3eb8f-157">Select **Create** to create your profile.</span></span> <span data-ttu-id="3eb8f-158">将在右下角显示一条消息，指示部署正在进行中。</span><span class="sxs-lookup"><span data-stu-id="3eb8f-158">A message appears in the lower-right corner indicating that deployment is in progress.</span></span> <span data-ttu-id="3eb8f-159">一小段时间后，将重新出现 "**发布**" 窗口。</span><span class="sxs-lookup"><span data-stu-id="3eb8f-159">After a short while, the **Publish** window reappears.</span></span>

    [![](part-1/_static/image17.png)](part-1/_static/image17.png)
   
    <span data-ttu-id="3eb8f-160">你创建的用于部署应用程序的配置文件现已可用。</span><span class="sxs-lookup"><span data-stu-id="3eb8f-160">The profile you created to deploy the app is now available.</span></span> 

> [!div class="step-by-step"]
> [<span data-ttu-id="3eb8f-161">下一部分</span><span class="sxs-lookup"><span data-stu-id="3eb8f-161">Next</span></span>](part-2.md)
