---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1
title: 第1部分：概述和文件-> 新项目 |Microsoft Docs
author: jongalloway
description: 本教程系列详细介绍了生成 ASP.NET MVC 音乐应用商店示例应用程序所需执行的所有步骤。 第1部分介绍了概述和文件 > 的新项目。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: bd356ca3-5bdb-4067-9dac-c9e9923a86e8
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1
msc.type: authoredcontent
ms.openlocfilehash: 48428ff4ab5888253ed93ac41e79006eec823ad2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78451280"
---
# <a name="part-1-overview-and-file-new-project"></a><span data-ttu-id="2eb2b-104">第1部分：概述和文件-> 新项目</span><span class="sxs-lookup"><span data-stu-id="2eb2b-104">Part 1: Overview and File->New Project</span></span>

<span data-ttu-id="2eb2b-105">作者： [Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="2eb2b-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="2eb2b-106">MVC 音乐应用商店是一个教程应用程序，该应用程序逐步介绍了如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发。</span><span class="sxs-lookup"><span data-stu-id="2eb2b-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="2eb2b-107">MVC 音乐应用商店是一种轻型示例存储实现，它可以在线销售音乐专辑，并实现基本的网站管理、用户登录和购物车功能。</span><span class="sxs-lookup"><span data-stu-id="2eb2b-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="2eb2b-108">本教程系列详细介绍了生成 ASP.NET MVC 音乐应用商店示例应用程序所需执行的所有步骤。</span><span class="sxs-lookup"><span data-stu-id="2eb2b-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="2eb2b-109">第1部分介绍了概述和文件&gt;的新项目。</span><span class="sxs-lookup"><span data-stu-id="2eb2b-109">Part 1 covers Overview and File-&gt;New Project.</span></span>

## <a name="overview"></a><span data-ttu-id="2eb2b-110">概述</span><span class="sxs-lookup"><span data-stu-id="2eb2b-110">Overview</span></span>

<span data-ttu-id="2eb2b-111">MVC 音乐应用商店是一个教程应用程序，该应用程序逐步介绍了如何使用 ASP.NET MVC 和用于 web 开发的 Visual Web Developer。</span><span class="sxs-lookup"><span data-stu-id="2eb2b-111">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Web Developer for web development.</span></span> <span data-ttu-id="2eb2b-112">我们将启动缓慢，因此初级级别的 web 开发体验一切正常。</span><span class="sxs-lookup"><span data-stu-id="2eb2b-112">We'll be starting slowly, so beginner level web development experience is okay.</span></span>

<span data-ttu-id="2eb2b-113">我们要构建的应用程序是一个简单的音乐应用商店。</span><span class="sxs-lookup"><span data-stu-id="2eb2b-113">The application we'll be building is a simple music store.</span></span> <span data-ttu-id="2eb2b-114">应用程序有三个主要部分：购物、结帐和管理。</span><span class="sxs-lookup"><span data-stu-id="2eb2b-114">There are three main parts to the application: shopping, checkout, and administration.</span></span>

![](mvc-music-store-part-1/_static/image1.jpg)

<span data-ttu-id="2eb2b-115">访问者可以按流派浏览唱片集：</span><span class="sxs-lookup"><span data-stu-id="2eb2b-115">Visitors can browse Albums by Genre:</span></span>

![](mvc-music-store-part-1/_static/image2.jpg)

<span data-ttu-id="2eb2b-116">他们可以查看单个唱片集并将其添加到购物车中：</span><span class="sxs-lookup"><span data-stu-id="2eb2b-116">They can view a single album and add it to their cart:</span></span>

![](mvc-music-store-part-1/_static/image3.jpg)

<span data-ttu-id="2eb2b-117">他们可以检查购物车，删除不再需要的任何项目：</span><span class="sxs-lookup"><span data-stu-id="2eb2b-117">They can review their cart, removing any items they no longer want:</span></span>

![](mvc-music-store-part-1/_static/image4.jpg)

<span data-ttu-id="2eb2b-118">继续结帐会提示他们登录或注册用户帐户。</span><span class="sxs-lookup"><span data-stu-id="2eb2b-118">Proceeding to Checkout will prompt them to login or register for a user account.</span></span>

![](mvc-music-store-part-1/_static/image1.png)

![](mvc-music-store-part-1/_static/image2.png)

<span data-ttu-id="2eb2b-119">创建帐户后，他们可以通过填写发货和付款信息来完成订单。</span><span class="sxs-lookup"><span data-stu-id="2eb2b-119">After creating an account, they can complete the order by filling out shipping and payment information.</span></span> <span data-ttu-id="2eb2b-120">为简单起见，我们正在运行精彩升级：如果他们输入促销代码 "免费"，则一切免费！</span><span class="sxs-lookup"><span data-stu-id="2eb2b-120">To keep things simple, we're running an amazing promotion: everything's free if they enter promotion code "FREE"!</span></span>

![](mvc-music-store-part-1/_static/image5.jpg)

<span data-ttu-id="2eb2b-121">排序后，他们会看到一个简单的确认屏幕：</span><span class="sxs-lookup"><span data-stu-id="2eb2b-121">After ordering, they see a simple confirmation screen:</span></span>

![](mvc-music-store-part-1/_static/image6.jpg)

<span data-ttu-id="2eb2b-122">除了面向客户的页面之外，我们还将生成一个 "管理员" 部分，其中显示了管理员可从中创建、编辑和删除唱片集的相册列表：</span><span class="sxs-lookup"><span data-stu-id="2eb2b-122">In addition to customer-facing pages, we'll also build an administrator section that shows a list of albums from which Administrators can Create, Edit, and Delete albums:</span></span>

![](mvc-music-store-part-1/_static/image7.jpg)

## <a name="1-file--gt-new-project"></a><span data-ttu-id="2eb2b-123">1. 文件-&gt; 新项目</span><span class="sxs-lookup"><span data-stu-id="2eb2b-123">1. File -&gt; New Project</span></span>

### <a name="installing-the-software"></a><span data-ttu-id="2eb2b-124">安装软件</span><span class="sxs-lookup"><span data-stu-id="2eb2b-124">Installing the software</span></span>

<span data-ttu-id="2eb2b-125">本教程将使用免费的 Visual Web Developer 2010 Express （免费）创建新的 ASP.NET MVC 3 项目，然后我们将以增量方式添加功能，以创建完整的正常运行的应用程序。</span><span class="sxs-lookup"><span data-stu-id="2eb2b-125">This tutorial will begin by creating a new ASP.NET MVC 3 project using the free Visual Web Developer 2010 Express (which is free), and then we'll incrementally add features to create a complete functioning application.</span></span> <span data-ttu-id="2eb2b-126">在此过程中，我们将介绍数据库访问、窗体发布方案、数据验证、使用母版页实现一致的页面布局、使用 AJAX 进行页面更新和验证、用户登录等等。</span><span class="sxs-lookup"><span data-stu-id="2eb2b-126">Along the way, we'll cover database access, form posting scenarios, data validation, using master pages for consistent page layout, using AJAX for page updates and validation, user login, and more.</span></span>

<span data-ttu-id="2eb2b-127">可以按照步骤进行操作，也可以从[MVC-音乐商店](https://github.com/evilDave/MVC-Music-Store)下载已完成的应用程序。</span><span class="sxs-lookup"><span data-stu-id="2eb2b-127">You can follow along step by step, or you can download the completed application from [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span>

<span data-ttu-id="2eb2b-128">可以使用 Visual Studio 2010 SP1 或 Visual Web Developer 2010 Express SP1 （Visual Studio 2010 的免费版本）来生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="2eb2b-128">You can use either Visual Studio 2010 SP1 or Visual Web Developer 2010 Express SP1 (a free version of Visual Studio 2010) to build the application.</span></span> <span data-ttu-id="2eb2b-129">我们将使用 SQL Server Compact （也是免费）来托管数据库。</span><span class="sxs-lookup"><span data-stu-id="2eb2b-129">We'll be using the SQL Server Compact (also free) to host the database.</span></span> <span data-ttu-id="2eb2b-130">在开始之前，请确保已安装下列必备组件。</span><span class="sxs-lookup"><span data-stu-id="2eb2b-130">Before you start, make sure you've installed the prerequisites listed below.</span></span>

- <span data-ttu-id="2eb2b-131">[Visual Studio Web Developer Express SP1 先决条件]</span><span class="sxs-lookup"><span data-stu-id="2eb2b-131">[Visual Studio Web Developer Express SP1 prerequisites]</span></span>
- <span data-ttu-id="2eb2b-132">[ASP.NET MVC 3 工具更新]</span><span class="sxs-lookup"><span data-stu-id="2eb2b-132">[ASP.NET MVC 3 Tools Update]</span></span>
- <span data-ttu-id="2eb2b-133">[SQL Server Compact 4.0]-包括运行时和工具支持</span><span class="sxs-lookup"><span data-stu-id="2eb2b-133">[SQL Server Compact 4.0] - including both runtime and tools support</span></span>

### <a name="creating-a-new-aspnet-mvc-3-project"></a><span data-ttu-id="2eb2b-134">创建新的 ASP.NET MVC 3 项目</span><span class="sxs-lookup"><span data-stu-id="2eb2b-134">Creating a new ASP.NET MVC 3 project</span></span>

<span data-ttu-id="2eb2b-135">首先，在 Visual Web Developer 的 "文件" 菜单中选择 "新建项目"。</span><span class="sxs-lookup"><span data-stu-id="2eb2b-135">We'll start by selecting "New Project" from the File menu in Visual Web Developer.</span></span> <span data-ttu-id="2eb2b-136">此时将打开 "新建项目" 对话框。</span><span class="sxs-lookup"><span data-stu-id="2eb2b-136">This brings up the New Project dialog.</span></span>

![](mvc-music-store-part-1/_static/image5.png)

<span data-ttu-id="2eb2b-137">选择左侧的 "视觉C#&gt; Web 模板" 组，然后在 "中心" 列中选择 "ASP.NET MVC 3 Web 应用程序" 模板。</span><span class="sxs-lookup"><span data-stu-id="2eb2b-137">We'll select the Visual C# -&gt; Web Templates group on the left, then choose the "ASP.NET MVC 3 Web Application" template in the center column.</span></span> <span data-ttu-id="2eb2b-138">将项目命名为 MvcMusicStore，然后按 "确定" 按钮。</span><span class="sxs-lookup"><span data-stu-id="2eb2b-138">Name your project MvcMusicStore and press the OK button.</span></span>

![](mvc-music-store-part-1/_static/image8.jpg)

<span data-ttu-id="2eb2b-139">这将显示一个辅助对话框，使我们可以为项目创建一些 MVC 特定的设置。</span><span class="sxs-lookup"><span data-stu-id="2eb2b-139">This will display a secondary dialog which allows us to make some MVC specific settings for our project.</span></span> <span data-ttu-id="2eb2b-140">选择以下项：</span><span class="sxs-lookup"><span data-stu-id="2eb2b-140">Select the following:</span></span>

<span data-ttu-id="2eb2b-141">项目模板-选择空</span><span class="sxs-lookup"><span data-stu-id="2eb2b-141">Project Template - select Empty</span></span>

<span data-ttu-id="2eb2b-142">查看引擎-选择 Razor</span><span class="sxs-lookup"><span data-stu-id="2eb2b-142">View Engine - select Razor</span></span>

<span data-ttu-id="2eb2b-143">使用 HTML5 语义标记-已选中</span><span class="sxs-lookup"><span data-stu-id="2eb2b-143">Use HTML5 semantic markup - checked</span></span>

<span data-ttu-id="2eb2b-144">验证你的设置如下所示，然后按 "确定" 按钮。</span><span class="sxs-lookup"><span data-stu-id="2eb2b-144">Verify that your settings are as shown below, then press the OK button.</span></span>

![](mvc-music-store-part-1/_static/image9.jpg)

<span data-ttu-id="2eb2b-145">这将创建项目。</span><span class="sxs-lookup"><span data-stu-id="2eb2b-145">This will create our project.</span></span> <span data-ttu-id="2eb2b-146">让我们看看在右侧的解决方案资源管理器中已添加到应用程序中的文件夹。</span><span class="sxs-lookup"><span data-stu-id="2eb2b-146">Let's take a look at the folders that have been added to our application in the Solution Explorer on the right side.</span></span>

![](mvc-music-store-part-1/_static/image10.jpg)

<span data-ttu-id="2eb2b-147">空 MVC 3 模板不完全为空-它会添加基本文件夹结构：</span><span class="sxs-lookup"><span data-stu-id="2eb2b-147">The Empty MVC 3 template isn't completely empty – it adds a basic folder structure:</span></span>

![](mvc-music-store-part-1/_static/image6.png)

<span data-ttu-id="2eb2b-148">ASP.NET MVC 对文件夹名称使用一些基本命名约定：</span><span class="sxs-lookup"><span data-stu-id="2eb2b-148">ASP.NET MVC makes use of some basic naming conventions for folder names:</span></span>

| <span data-ttu-id="2eb2b-149">**文件夹**</span><span class="sxs-lookup"><span data-stu-id="2eb2b-149">**Folder**</span></span> | <span data-ttu-id="2eb2b-150">**目的**</span><span class="sxs-lookup"><span data-stu-id="2eb2b-150">**Purpose**</span></span> |
| --- | --- |
| <span data-ttu-id="2eb2b-151">**/Controllers**</span><span class="sxs-lookup"><span data-stu-id="2eb2b-151">**/Controllers**</span></span> | <span data-ttu-id="2eb2b-152">控制器响应浏览器的输入，决定要如何处理它，并向用户返回响应。</span><span class="sxs-lookup"><span data-stu-id="2eb2b-152">Controllers respond to input from the browser, decide what to do with it, and return response to the user.</span></span> |
| <span data-ttu-id="2eb2b-153">**/Views**</span><span class="sxs-lookup"><span data-stu-id="2eb2b-153">**/Views**</span></span> | <span data-ttu-id="2eb2b-154">视图保存我们的 UI 模板</span><span class="sxs-lookup"><span data-stu-id="2eb2b-154">Views hold our UI templates</span></span> |
| <span data-ttu-id="2eb2b-155">**/Models**</span><span class="sxs-lookup"><span data-stu-id="2eb2b-155">**/Models**</span></span> | <span data-ttu-id="2eb2b-156">模型保存和操作数据</span><span class="sxs-lookup"><span data-stu-id="2eb2b-156">Models hold and manipulate data</span></span> |
| <span data-ttu-id="2eb2b-157">**/Content**</span><span class="sxs-lookup"><span data-stu-id="2eb2b-157">**/Content**</span></span> | <span data-ttu-id="2eb2b-158">此文件夹包含图像、CSS 和任何其他静态内容</span><span class="sxs-lookup"><span data-stu-id="2eb2b-158">This folder holds our images, CSS, and any other static content</span></span> |
| <span data-ttu-id="2eb2b-159">**/Scripts**</span><span class="sxs-lookup"><span data-stu-id="2eb2b-159">**/Scripts**</span></span> | <span data-ttu-id="2eb2b-160">此文件夹包含 JavaScript 文件</span><span class="sxs-lookup"><span data-stu-id="2eb2b-160">This folder holds our JavaScript files</span></span> |

<span data-ttu-id="2eb2b-161">即使在空的 ASP.NET MVC 应用程序中也包含这些文件夹，因为 ASP.NET MVC 框架默认情况下使用 "约定 over 配置" 方法，并基于文件夹命名约定做出一些默认假设。</span><span class="sxs-lookup"><span data-stu-id="2eb2b-161">These folders are included even in an Empty ASP.NET MVC application because the ASP.NET MVC framework by default uses a "convention over configuration" approach and makes some default assumptions based on folder naming conventions.</span></span> <span data-ttu-id="2eb2b-162">例如，默认情况下，控制器将在 Views 文件夹中查找视图，无需在代码中显式指定此项。</span><span class="sxs-lookup"><span data-stu-id="2eb2b-162">For instance, controllers look for views in the Views folder by default without you having to explicitly specify this in your code.</span></span> <span data-ttu-id="2eb2b-163">坚持默认约定会减少需要编写的代码量，还可以使其他开发人员更容易了解你的项目。</span><span class="sxs-lookup"><span data-stu-id="2eb2b-163">Sticking with the default conventions reduces the amount of code you need to write, and can also make it easier for other developers to understand your project.</span></span> <span data-ttu-id="2eb2b-164">在构建应用程序时，我们将更详细地介绍这些约定。</span><span class="sxs-lookup"><span data-stu-id="2eb2b-164">We'll explain these conventions more as we build our application.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="2eb2b-165">下一部分</span><span class="sxs-lookup"><span data-stu-id="2eb2b-165">Next</span></span>](mvc-music-store-part-2.md)
