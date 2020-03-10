---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-1
title: 第1部分：文件-> 新项目 |Microsoft Docs
author: JoeStagner
description: 本教程系列详细介绍了生成 Tailspin Spyworks 示例应用程序所需执行的所有步骤。 第1部分介绍了概述和文件/新项目。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 15d4652b-d5aa-4172-b186-2c7f96ba316d
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-1
msc.type: authoredcontent
ms.openlocfilehash: 05a3ace3d8fef9c1f3593f7948e42b4725d70134
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78516536"
---
# <a name="part-1-file--new-project"></a><span data-ttu-id="8b5a2-104">第1部分：文件-> 新项目</span><span class="sxs-lookup"><span data-stu-id="8b5a2-104">Part 1: File-> New Project</span></span>

<span data-ttu-id="8b5a2-105">作者： [Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="8b5a2-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="8b5a2-106">Tailspin Spyworks 演示了创建适用于 .NET 平台的功能强大的可缩放应用程序是多么简单。</span><span class="sxs-lookup"><span data-stu-id="8b5a2-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="8b5a2-107">其中展示了如何使用 ASP.NET 4 中的优秀新功能构建在线商店，包括购物、结帐和管理。</span><span class="sxs-lookup"><span data-stu-id="8b5a2-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="8b5a2-108">本教程系列详细介绍了生成 Tailspin Spyworks 示例应用程序所需执行的所有步骤。</span><span class="sxs-lookup"><span data-stu-id="8b5a2-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="8b5a2-109">第1部分介绍了概述和文件/新项目。</span><span class="sxs-lookup"><span data-stu-id="8b5a2-109">Part 1 covers Overview and File/New Project.</span></span>

## <a id="_Toc260221666"></a><span data-ttu-id="8b5a2-110">叙述</span><span class="sxs-lookup"><span data-stu-id="8b5a2-110">Overview</span></span>

<span data-ttu-id="8b5a2-111">本教程介绍了 ASP.NET WebForms。</span><span class="sxs-lookup"><span data-stu-id="8b5a2-111">This tutorial is an introduction to ASP.NET WebForms.</span></span> <span data-ttu-id="8b5a2-112">我们将启动缓慢，因此初级级别的 web 开发体验一切正常。</span><span class="sxs-lookup"><span data-stu-id="8b5a2-112">We'll be starting slowly, so beginner level web development experience is okay.</span></span>

<span data-ttu-id="8b5a2-113">我们要构建的应用程序是一个简单的在线商店。</span><span class="sxs-lookup"><span data-stu-id="8b5a2-113">The application we'll be building is a simple on-line store.</span></span>

![](tailspin-spyworks-part-1/_static/image1.jpg)

<span data-ttu-id="8b5a2-114">访问者可以按类别浏览产品：</span><span class="sxs-lookup"><span data-stu-id="8b5a2-114">Visitors can browse Products by Category:</span></span>

![](tailspin-spyworks-part-1/_static/image2.jpg)

<span data-ttu-id="8b5a2-115">他们可以查看单个产品并将其添加到购物车中：</span><span class="sxs-lookup"><span data-stu-id="8b5a2-115">They can view a single product and add it to their cart:</span></span>

![](tailspin-spyworks-part-1/_static/image3.jpg)

<span data-ttu-id="8b5a2-116">他们可以检查购物车，删除不再需要的任何项目：</span><span class="sxs-lookup"><span data-stu-id="8b5a2-116">They can review their cart, removing any items they no longer want:</span></span>

![](tailspin-spyworks-part-1/_static/image4.jpg)

<span data-ttu-id="8b5a2-117">继续结帐会提示他们</span><span class="sxs-lookup"><span data-stu-id="8b5a2-117">Proceeding to Checkout will prompt them to</span></span>

![](tailspin-spyworks-part-1/_static/image5.jpg)

![](tailspin-spyworks-part-1/_static/image6.jpg)

<span data-ttu-id="8b5a2-118">排序后，他们会看到一个简单的确认屏幕：</span><span class="sxs-lookup"><span data-stu-id="8b5a2-118">After ordering, they see a simple confirmation screen:</span></span>

![](tailspin-spyworks-part-1/_static/image7.jpg)

<span data-ttu-id="8b5a2-119">首先，我们将在 Visual Studio 2010 中创建新的 ASP.NET WebForms 项目，并以增量方式添加功能，以创建完整的正常运行的应用程序。</span><span class="sxs-lookup"><span data-stu-id="8b5a2-119">We'll begin by creating a new ASP.NET WebForms project in Visual Studio 2010, and we'll incrementally add features to create a complete functioning application.</span></span> <span data-ttu-id="8b5a2-120">在此过程中，我们将介绍数据库访问、列表和网格视图、数据更新页面、数据验证、使用母版页以实现一致的页面布局、AJAX、验证、用户成员身份等。</span><span class="sxs-lookup"><span data-stu-id="8b5a2-120">Along the way, we'll cover database access, list and grid views, data update pages, data validation, using master pages for consistent page layout, AJAX, validation, user membership, and more.</span></span>

<span data-ttu-id="8b5a2-121">可以按照步骤进行操作，也可以从[http://tailspinspyworks.codeplex.com/](http://tailspinspyworks.codeplex.com/)下载已完成的应用程序。</span><span class="sxs-lookup"><span data-stu-id="8b5a2-121">You can follow along step by step, or you can download the completed application from [http://tailspinspyworks.codeplex.com/](http://tailspinspyworks.codeplex.com/)</span></span>

<span data-ttu-id="8b5a2-122">可以从[https://www.microsoft.com/express/Web/](https://www.microsoft.com/express/Web/)使用 visual Studio 2010 或免费的 Visual Web Developer 2010。</span><span class="sxs-lookup"><span data-stu-id="8b5a2-122">You can use either Visual Studio 2010 or the free Visual Web Developer 2010 from [https://www.microsoft.com/express/Web/](https://www.microsoft.com/express/Web/).</span></span> <span data-ttu-id="8b5a2-123">若要生成应用程序，可以使用 SQL Server 或免费 SQL Server Express 来托管数据库。</span><span class="sxs-lookup"><span data-stu-id="8b5a2-123">To build the application, you can use either SQL Server or the free SQL Server Express to host the database.</span></span>

## <a id="_Toc260221667"></a><span data-ttu-id="8b5a2-124">文件/新建项目</span><span class="sxs-lookup"><span data-stu-id="8b5a2-124">File / New Project</span></span>

<span data-ttu-id="8b5a2-125">首先从 Visual Studio 中的 "文件" 菜单中选择新项目。</span><span class="sxs-lookup"><span data-stu-id="8b5a2-125">We'll start by selecting the New Project from the File menu in Visual Studio.</span></span> <span data-ttu-id="8b5a2-126">此时将打开 "新建项目" 对话框。</span><span class="sxs-lookup"><span data-stu-id="8b5a2-126">This brings up the New Project dialog.</span></span>

![](tailspin-spyworks-part-1/_static/image8.jpg)

<span data-ttu-id="8b5a2-127">选择左侧的 "视觉C#对象"/"web 模板" 组，然后在 "中心" 列中选择 "ASP.NET Web 应用程序" 模板。</span><span class="sxs-lookup"><span data-stu-id="8b5a2-127">We'll select the Visual C# / Web Templates group on the left, and then choose the "ASP.NET Web Application" template in the center column.</span></span> <span data-ttu-id="8b5a2-128">将项目命名为 TailspinSpyworks，然后按 "确定" 按钮。</span><span class="sxs-lookup"><span data-stu-id="8b5a2-128">Name your project TailspinSpyworks and press the OK button.</span></span>

![](tailspin-spyworks-part-1/_static/image9.jpg)

<span data-ttu-id="8b5a2-129">这将创建项目。</span><span class="sxs-lookup"><span data-stu-id="8b5a2-129">This will create our project.</span></span> <span data-ttu-id="8b5a2-130">让我们看看应用程序中包含的文件夹，这些文件夹位于右侧的解决方案资源管理器中。</span><span class="sxs-lookup"><span data-stu-id="8b5a2-130">Let's take a look at the folders that are included in our application in the Solution Explorer on the right side.</span></span>

![](tailspin-spyworks-part-1/_static/image10.jpg)

<span data-ttu-id="8b5a2-131">空解决方案不完全为空-它添加了一个基本文件夹结构：</span><span class="sxs-lookup"><span data-stu-id="8b5a2-131">The Empty Solution isn't completely empty – it adds a basic folder structure:</span></span>

![](tailspin-spyworks-part-1/_static/image1.png)

<span data-ttu-id="8b5a2-132">请注意 ASP.NET 4 默认项目模板实现的约定。</span><span class="sxs-lookup"><span data-stu-id="8b5a2-132">Note the conventions implemented by the ASP.NET 4 default project template.</span></span>

- <span data-ttu-id="8b5a2-133">"帐户" 文件夹实现了 ASP 的基本用户界面。网络的成员资格子系统。</span><span class="sxs-lookup"><span data-stu-id="8b5a2-133">The "Account" folder implements a basic user interface for ASP.NET's membership subsystem.</span></span>
- <span data-ttu-id="8b5a2-134">"脚本" 文件夹将用作客户端 JavaScript 文件的存储库，并且默认情况下将提供 core jQuery .js 文件。</span><span class="sxs-lookup"><span data-stu-id="8b5a2-134">The "Scripts" folder serves as the repository for client side JavaScript files and the core jQuery .js files are made available by default.</span></span>
- <span data-ttu-id="8b5a2-135">"样式" 文件夹用于组织网站视觉对象（CSS 样式表）</span><span class="sxs-lookup"><span data-stu-id="8b5a2-135">The "Styles" folder is used to organize our web site visuals (CSS Style Sheets)</span></span>

<span data-ttu-id="8b5a2-136">如果按 F5 运行应用程序并呈现 default.aspx 页，将看到以下各项。</span><span class="sxs-lookup"><span data-stu-id="8b5a2-136">When we press F5 to run our application and render the default.aspx page we see the following.</span></span>

![](tailspin-spyworks-part-1/_static/image11.jpg)

<span data-ttu-id="8b5a2-137">第一次应用程序增强功能是将默认 WebForms 模板中的 Style .css 文件替换为 CSS 类和关联的图像文件，这些文件将呈现我们的 Tailspin Spyworks 应用程序所需的视觉对象 asthetics。</span><span class="sxs-lookup"><span data-stu-id="8b5a2-137">Our first application enhancement will be to replace the Style.css file from the default WebForms template with the CSS classes and associated image files that will render the visual asthetics that we want for our Tailspin Spyworks application.</span></span>

<span data-ttu-id="8b5a2-138">完成此操作后，我们的默认 .aspx 页面将呈现为此。</span><span class="sxs-lookup"><span data-stu-id="8b5a2-138">After doing so our default.aspx page renders like this.</span></span>

![](tailspin-spyworks-part-1/_static/image12.jpg)

<span data-ttu-id="8b5a2-139">请注意页面右上角的图像链接和已添加到母版页的菜单项。</span><span class="sxs-lookup"><span data-stu-id="8b5a2-139">Notice the image links at the top right of the page and the menu items that have been added to the master page.</span></span> <span data-ttu-id="8b5a2-140">只有 "登录" 和 "帐户" 链接指向存在的页面（由默认模板生成）以及我们将在构建应用程序时实现的其余页面。</span><span class="sxs-lookup"><span data-stu-id="8b5a2-140">Only the "Sign In" and "Account" links point to pages that exist (generated by the default template) and the rest of the pages we will implement as we build our application.</span></span>

<span data-ttu-id="8b5a2-141">我们还将母版页定位到样式目录。</span><span class="sxs-lookup"><span data-stu-id="8b5a2-141">We're also going to relocate the Master Page to the Styles directory.</span></span> <span data-ttu-id="8b5a2-142">尽管这只是一个首选项，但如果我们决定以后让应用程序 "skinable"，则可能会变得更容易。</span><span class="sxs-lookup"><span data-stu-id="8b5a2-142">Though this is only a preference it may make things a little easier if we decide to make our application "skinable" in the future.</span></span>

<span data-ttu-id="8b5a2-143">完成此操作后，我们需要更改默认 ASP.NET WebForms 页面生成的所有 .aspx 文件中的母版页引用。</span><span class="sxs-lookup"><span data-stu-id="8b5a2-143">After doing this we'll need to change the master page references in all the .aspx files generated by the default ASP.NET WebForms pages.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="8b5a2-144">下一部分</span><span class="sxs-lookup"><span data-stu-id="8b5a2-144">Next</span></span>](tailspin-spyworks-part-2.md)
