---
uid: mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
title: NerdDinner 教程简介 |Microsoft Docs
author: shanselman
description: 了解新框架的最佳方式是使用它来构建一些内容。 本教程介绍如何使用 ASP.NE 构建小型但完整的应用程序 。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 397522d5-0402-4b94-b810-a2fb564f869d
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
msc.type: authoredcontent
ms.openlocfilehash: 154cfe6694cf723c0a1f8e33bfdb42c97594518f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468932"
---
# <a name="introducing-the-nerddinner-tutorial"></a><span data-ttu-id="0d491-104">NerdDinner 教程简介</span><span class="sxs-lookup"><span data-stu-id="0d491-104">Introducing the NerdDinner Tutorial</span></span>

<span data-ttu-id="0d491-105">作者： [Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="0d491-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

[<span data-ttu-id="0d491-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="0d491-106">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="0d491-107">了解新框架的最佳方式是使用它来构建一些内容。</span><span class="sxs-lookup"><span data-stu-id="0d491-107">The best way to learn a new framework is to build something with it.</span></span> <span data-ttu-id="0d491-108">本教程介绍如何使用 ASP.NET MVC 1 构建小型但完整的应用程序，并介绍了其背后的一些核心概念。</span><span class="sxs-lookup"><span data-stu-id="0d491-108">This tutorial walks through how to build a small, but complete, application using ASP.NET MVC 1, and introduces some of the core concepts behind it.</span></span>
> 
> <span data-ttu-id="0d491-109">如果你使用的是 ASP.NET MVC 3，则建议你遵循[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[Mvc 音乐应用商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程中的入门。</span><span class="sxs-lookup"><span data-stu-id="0d491-109">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-tutorial"></a><span data-ttu-id="0d491-110">NerdDinner 教程</span><span class="sxs-lookup"><span data-stu-id="0d491-110">NerdDinner Tutorial</span></span>

<span data-ttu-id="0d491-111">了解新框架的最佳方式是使用它来构建一些内容。</span><span class="sxs-lookup"><span data-stu-id="0d491-111">The best way to learn a new framework is to build something with it.</span></span> <span data-ttu-id="0d491-112">本教程介绍如何使用 ASP.NET MVC 构建小型但完整的应用程序，并介绍了其背后的一些核心概念。</span><span class="sxs-lookup"><span data-stu-id="0d491-112">This tutorial walks through how to build a small, but complete, application using ASP.NET MVC, and introduces some of the core concepts behind it.</span></span>

<span data-ttu-id="0d491-113">要生成的应用程序称为 "NerdDinner"。</span><span class="sxs-lookup"><span data-stu-id="0d491-113">The application we are going to build is called "NerdDinner".</span></span> <span data-ttu-id="0d491-114">NerdDinner 提供了一种简单的方法，使用户能够轻松查找和组织就：</span><span class="sxs-lookup"><span data-stu-id="0d491-114">NerdDinner provides an easy way for people to find and organize dinners online:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image1.png)

<span data-ttu-id="0d491-115">NerdDinner 允许注册用户创建、编辑和删除就。</span><span class="sxs-lookup"><span data-stu-id="0d491-115">NerdDinner enables registered users to create, edit and delete dinners.</span></span> <span data-ttu-id="0d491-116">它在应用程序中强制实施一组一致的验证和业务规则：</span><span class="sxs-lookup"><span data-stu-id="0d491-116">It enforces a consistent set of validation and business rules across the application:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image2.png)

<span data-ttu-id="0d491-117">访问者可以使用基于 AJAX 的地图来搜索即将发布的就：</span><span class="sxs-lookup"><span data-stu-id="0d491-117">Visitors can use an AJAX-based map to search for upcoming dinners being held near them:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image3.png)

<span data-ttu-id="0d491-118">单击晚餐会将其转到详细信息页面，用户可在其中了解更多相关信息：</span><span class="sxs-lookup"><span data-stu-id="0d491-118">Clicking a dinner will take them to a details page where they can learn more about it:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image4.png)

<span data-ttu-id="0d491-119">如果他们感兴趣，他们可以在网站上登录或注册：</span><span class="sxs-lookup"><span data-stu-id="0d491-119">If they are interested in attending the dinner they can login or register on the site:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image5.png)

<span data-ttu-id="0d491-120">然后，他们可以单击基于 AJAX 的 RSVP 链接参加事件：</span><span class="sxs-lookup"><span data-stu-id="0d491-120">They can then click an AJAX-based RSVP link to attend the event:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image6.png)

![](introducing-the-nerddinner-tutorial/_static/image7.png)

### <a name="implementing-nerddinner"></a><span data-ttu-id="0d491-121">实现 NerdDinner</span><span class="sxs-lookup"><span data-stu-id="0d491-121">Implementing NerdDinner</span></span>

<span data-ttu-id="0d491-122">接下来，我们将使用 Visual Studio 中的 "文件&gt;" 新建项目 "命令来创建全新的 ASP.NET MVC 项目。</span><span class="sxs-lookup"><span data-stu-id="0d491-122">We are going to begin our NerdDinner application by using the File-&gt;New Project command within Visual Studio to create a brand new ASP.NET MVC project.</span></span> <span data-ttu-id="0d491-123">然后，我们将增量添加功能和功能。</span><span class="sxs-lookup"><span data-stu-id="0d491-123">We will then incrementally add functionality and features.</span></span> <span data-ttu-id="0d491-124">在此过程中，我们将介绍：</span><span class="sxs-lookup"><span data-stu-id="0d491-124">Along the way we'll cover:</span></span>

1. [<span data-ttu-id="0d491-125">如何创建新的 ASP.NET MVC 项目</span><span class="sxs-lookup"><span data-stu-id="0d491-125">How to create a new ASP.NET MVC Project</span></span>](create-a-new-aspnet-mvc-project.md)
2. [<span data-ttu-id="0d491-126">如何创建数据库</span><span class="sxs-lookup"><span data-stu-id="0d491-126">How to create a database</span></span>](create-a-database.md)
3. [<span data-ttu-id="0d491-127">如何使用业务规则验证生成模型</span><span class="sxs-lookup"><span data-stu-id="0d491-127">How to build a model with business rule validations</span></span>](build-a-model-with-business-rule-validations.md)
4. [<span data-ttu-id="0d491-128">如何使用控制器和视图实现列表/详细信息 UI</span><span class="sxs-lookup"><span data-stu-id="0d491-128">How to use controllers and views to implement a listing/details UI</span></span>](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
5. [<span data-ttu-id="0d491-129">如何提供 CRUD （创建、读取、更新、删除）数据表单条目支持</span><span class="sxs-lookup"><span data-stu-id="0d491-129">How to provide CRUD (create, read, update, delete) data form entry support</span></span>](provide-crud-create-read-update-delete-data-form-entry-support.md)
6. [<span data-ttu-id="0d491-130">如何使用 ViewData 和实现 ViewModel 类</span><span class="sxs-lookup"><span data-stu-id="0d491-130">How to use ViewData and implement ViewModel classes</span></span>](use-viewdata-and-implement-viewmodel-classes.md)
7. [<span data-ttu-id="0d491-131">如何使用母版页和分区重新使用 UI</span><span class="sxs-lookup"><span data-stu-id="0d491-131">How to re-use UI using master pages and partials</span></span>](re-use-ui-using-master-pages-and-partials.md)
8. [<span data-ttu-id="0d491-132">如何实现高效的数据分页</span><span class="sxs-lookup"><span data-stu-id="0d491-132">How to implement efficient data paging</span></span>](implement-efficient-data-paging.md)
9. [<span data-ttu-id="0d491-133">如何使用身份验证和授权保护应用程序</span><span class="sxs-lookup"><span data-stu-id="0d491-133">How to secure applications using authentication and authorization</span></span>](secure-applications-using-authentication-and-authorization.md)
10. [<span data-ttu-id="0d491-134">如何使用 AJAX 交付动态更新</span><span class="sxs-lookup"><span data-stu-id="0d491-134">How to use AJAX to deliver dynamic updates</span></span>](use-ajax-to-deliver-dynamic-updates.md)
11. [<span data-ttu-id="0d491-135">如何使用 AJAX 实现映射方案</span><span class="sxs-lookup"><span data-stu-id="0d491-135">How to use AJAX to implement mapping scenarios</span></span>](use-ajax-to-implement-mapping-scenarios.md)
12. [<span data-ttu-id="0d491-136">如何启用自动单元测试</span><span class="sxs-lookup"><span data-stu-id="0d491-136">How to enable automated unit testing</span></span>](enable-automated-unit-testing.md)

<span data-ttu-id="0d491-137">你可以通过完成本章节中演练的每个步骤，从头开始生成你自己的 NerdDinner 副本。</span><span class="sxs-lookup"><span data-stu-id="0d491-137">You can build your own copy of NerdDinner from scratch by completing each step we walkthrough in this chapter.</span></span> <span data-ttu-id="0d491-138">或者，你可以在[GitHub 上](https://github.com/AspNetMVPSamples/NerdDinner)的以下位置下载源代码的完整版本： NerdDinner。</span><span class="sxs-lookup"><span data-stu-id="0d491-138">Alternatively, you can download a completed version of the source code here: [NerdDinner on GitHub](https://github.com/AspNetMVPSamples/NerdDinner).</span></span> <span data-ttu-id="0d491-139">如果你想要脱机阅读本教程，还可以选择[下载本教程的免费 PDF 版本](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)。</span><span class="sxs-lookup"><span data-stu-id="0d491-139">You can also optionally also [download a free PDF version of this tutorial](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf) if you want to read the tutorial offline.</span></span>

<span data-ttu-id="0d491-140">可以使用 Visual Studio 2008 或免费的 Visual Web Developer 2008 Express 来生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="0d491-140">You can use either Visual Studio 2008 or the free Visual Web Developer 2008 Express to build the application.</span></span> <span data-ttu-id="0d491-141">您可以使用数据库的 SQL Server 或免费 SQL Server Express。</span><span class="sxs-lookup"><span data-stu-id="0d491-141">You can use either SQL Server or the free SQL Server Express for the database.</span></span>

<span data-ttu-id="0d491-142">你可以使用[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)的 V2 安装 ASP.NET MVC、Visual Web Developer 2008 Express 和 SQL Server Express （免费）</span><span class="sxs-lookup"><span data-stu-id="0d491-142">You can install ASP.NET MVC, Visual Web Developer 2008 Express, and SQL Server Express (all free) using V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)</span></span>

### <a name="now-lets-get-started"></a><span data-ttu-id="0d491-143">现在让我们开始吧 ... 。</span><span class="sxs-lookup"><span data-stu-id="0d491-143">Now let's get started....</span></span>

<span data-ttu-id="0d491-144">现在我们已介绍了哪些 NerdDinner，让我们来汇总我们的卷起，并编写一些代码。</span><span class="sxs-lookup"><span data-stu-id="0d491-144">Now that we've covered what NerdDinner is, let's roll up our sleeves and write some code.</span></span>

<span data-ttu-id="0d491-145">首先，我们将使用 Visual Studio 中的文件&gt;新项目来创建 NerdDinner 应用程序。</span><span class="sxs-lookup"><span data-stu-id="0d491-145">We'll begin by using File-&gt;New Project within Visual Studio to create the NerdDinner application.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="0d491-146">下一部分</span><span class="sxs-lookup"><span data-stu-id="0d491-146">Next</span></span>](create-a-new-aspnet-mvc-project.md)
