---
uid: mvc/overview/older-versions-1/movie-database/create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs
title: 使用 ASP.NET MVC （C#）在15分钟内创建电影数据库应用程序 |Microsoft Docs
author: StephenWalther
description: Stephen Walther 从头开始构建整个数据库驱动的 ASP.NET MVC 应用程序。 本教程非常介绍了新的 t 。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: dd1be137-91c5-47a8-8137-fecf0789c7f5
msc.legacyurl: /mvc/overview/older-versions-1/movie-database/create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs
msc.type: authoredcontent
ms.openlocfilehash: 1be5d135a44feb27626dd26a544b64cfb57b18a9
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74596363"
---
# <a name="create-a-movie-database-application-in-15-minutes-with-aspnet-mvc-c"></a><span data-ttu-id="2af27-104">使用 ASP.NET MVC 在 15 分钟内创建电影数据库应用程序 (C#)</span><span class="sxs-lookup"><span data-stu-id="2af27-104">Create a Movie Database Application in 15 Minutes with ASP.NET MVC (C#)</span></span>

<span data-ttu-id="2af27-105">作者： [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="2af27-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

[<span data-ttu-id="2af27-106">下载代码</span><span class="sxs-lookup"><span data-stu-id="2af27-106">Download Code</span></span>](https://download.microsoft.com/download/7/2/8/728F8794-E59A-4D18-9A56-7AD2DB05BD9D/MovieApp_CS.zip)

> <span data-ttu-id="2af27-107">Stephen Walther 从头开始构建整个数据库驱动的 ASP.NET MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="2af27-107">Stephen Walther builds an entire database-driven ASP.NET MVC application from start to finish.</span></span> <span data-ttu-id="2af27-108">本教程非常介绍了 ASP.NET MVC 框架的新手，并希望了解构建 ASP.NET MVC 应用程序的过程。</span><span class="sxs-lookup"><span data-stu-id="2af27-108">This tutorial is a great introduction for people who are new to the ASP.NET MVC Framework and who want to get a sense of the process of building an ASP.NET MVC application.</span></span>

<span data-ttu-id="2af27-109">本教程的目的是让你了解一下如何构建 ASP.NET MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="2af27-109">The purpose of this tutorial is to give you a sense of "what it is like" to build an ASP.NET MVC application.</span></span> <span data-ttu-id="2af27-110">在本教程中，我将从开始到完成构建整个 ASP.NET MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="2af27-110">In this tutorial, I blast through building an entire ASP.NET MVC application from start to finish.</span></span> <span data-ttu-id="2af27-111">我向您展示了如何构建一个简单的数据库驱动的应用程序，该应用程序说明了如何列出、创建和编辑数据库记录。</span><span class="sxs-lookup"><span data-stu-id="2af27-111">I show you how to build a simple database-driven application that illustrates how you can list, create, and edit database records.</span></span>

<span data-ttu-id="2af27-112">为了简化生成应用程序的过程，我们将利用 Visual Studio 2008 的基架功能。</span><span class="sxs-lookup"><span data-stu-id="2af27-112">To simplify the process of building our application, we'll take advantage of the scaffolding features of Visual Studio 2008.</span></span> <span data-ttu-id="2af27-113">我们会让 Visual Studio 为控制器、模型和视图生成初始代码和内容。</span><span class="sxs-lookup"><span data-stu-id="2af27-113">We'll let Visual Studio generate the initial code and content for our controllers, models, and views.</span></span>

<span data-ttu-id="2af27-114">如果你使用的是 Active Server Pages 或 ASP.NET，则应该会发现 ASP.NET MVC 非常熟悉。</span><span class="sxs-lookup"><span data-stu-id="2af27-114">If you have worked with Active Server Pages or ASP.NET, then you should find ASP.NET MVC very familiar.</span></span> <span data-ttu-id="2af27-115">ASP.NET MVC 视图非常类似于 Active Server Pages 应用程序中的页面。</span><span class="sxs-lookup"><span data-stu-id="2af27-115">ASP.NET MVC views are very much like the pages in an Active Server Pages application.</span></span> <span data-ttu-id="2af27-116">与传统的 ASP.NET Web 窗体应用程序一样，ASP.NET MVC 为你提供 .NET framework 提供的丰富语言和类的完全访问权限。</span><span class="sxs-lookup"><span data-stu-id="2af27-116">And, just like a traditional ASP.NET Web Forms application, ASP.NET MVC provides you with full access to the rich set of languages and classes provided by the .NET framework.</span></span>

<span data-ttu-id="2af27-117">我希望在本教程中，您可以了解构建 ASP.NET MVC 应用程序的体验与生成 Active Server Pages 或 ASP.NET Web 窗体应用程序的体验是类似的。</span><span class="sxs-lookup"><span data-stu-id="2af27-117">My hope is that this tutorial will give you a sense of how the experience of building an ASP.NET MVC application is both similar and different than the experience of building an Active Server Pages or ASP.NET Web Forms application.</span></span>

## <a name="overview-of-the-movie-database-application"></a><span data-ttu-id="2af27-118">电影数据库应用程序概述</span><span class="sxs-lookup"><span data-stu-id="2af27-118">Overview of the Movie Database Application</span></span>

<span data-ttu-id="2af27-119">由于我们的目标是简单起见，我们将构建一个非常简单的电影数据库应用程序。</span><span class="sxs-lookup"><span data-stu-id="2af27-119">Because our goal is to keep things simple, we'll build a very simple Movie Database application.</span></span> <span data-ttu-id="2af27-120">简单的电影数据库应用程序将允许我们执行以下三项操作：</span><span class="sxs-lookup"><span data-stu-id="2af27-120">Our simple Movie Database application will allow us to do three things:</span></span>

1. <span data-ttu-id="2af27-121">列出一组电影数据库记录</span><span class="sxs-lookup"><span data-stu-id="2af27-121">List a set of movie database records</span></span>
2. <span data-ttu-id="2af27-122">创建新的电影数据库记录</span><span class="sxs-lookup"><span data-stu-id="2af27-122">Create a new movie database record</span></span>
3. <span data-ttu-id="2af27-123">编辑现有的电影数据库记录</span><span class="sxs-lookup"><span data-stu-id="2af27-123">Edit an existing movie database record</span></span>

<span data-ttu-id="2af27-124">同样，由于我们想要简单简单，我们将利用构建应用程序所需的 ASP.NET MVC 框架的最小功能数。</span><span class="sxs-lookup"><span data-stu-id="2af27-124">Again, because we want to keep things simple, we'll take advantage of the minimum number of features of the ASP.NET MVC framework needed to build our application.</span></span> <span data-ttu-id="2af27-125">例如，我们不会利用测试驱动的开发。</span><span class="sxs-lookup"><span data-stu-id="2af27-125">For example, we won't be taking advantage of Test-Driven Development.</span></span>

<span data-ttu-id="2af27-126">若要创建应用程序，需要完成以下每个步骤：</span><span class="sxs-lookup"><span data-stu-id="2af27-126">In order to create our application, we need to complete each of the following steps:</span></span>

1. <span data-ttu-id="2af27-127">创建 ASP.NET MVC Web 应用程序项目</span><span class="sxs-lookup"><span data-stu-id="2af27-127">Create the ASP.NET MVC Web Application Project</span></span>
2. <span data-ttu-id="2af27-128">创建数据库</span><span class="sxs-lookup"><span data-stu-id="2af27-128">Create the database</span></span>
3. <span data-ttu-id="2af27-129">创建数据库模型</span><span class="sxs-lookup"><span data-stu-id="2af27-129">Create the database model</span></span>
4. <span data-ttu-id="2af27-130">创建 ASP.NET MVC 控制器</span><span class="sxs-lookup"><span data-stu-id="2af27-130">Create the ASP.NET MVC controller</span></span>
5. <span data-ttu-id="2af27-131">创建 ASP.NET MVC 视图</span><span class="sxs-lookup"><span data-stu-id="2af27-131">Create the ASP.NET MVC views</span></span>

## <a name="preliminaries"></a><span data-ttu-id="2af27-132">初步</span><span class="sxs-lookup"><span data-stu-id="2af27-132">Preliminaries</span></span>

<span data-ttu-id="2af27-133">需要 Visual Studio 2008 或 Visual Web Developer 2008 Express 才能生成 ASP.NET MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="2af27-133">You'll need either Visual Studio 2008 or Visual Web Developer 2008 Express to build an ASP.NET MVC application.</span></span> <span data-ttu-id="2af27-134">还需要下载 ASP.NET MVC 框架。</span><span class="sxs-lookup"><span data-stu-id="2af27-134">You also need to download the ASP.NET MVC framework.</span></span>

<span data-ttu-id="2af27-135">如果你没有 Visual Studio 2008，你可以从以下网站90下载试用版的 Visual Studio 2008：</span><span class="sxs-lookup"><span data-stu-id="2af27-135">If you don't own Visual Studio 2008, then you can download a 90 day trial version of Visual Studio 2008 from this website:</span></span>

[https://msdn.microsoft.com/vs2008/products/cc268305.aspx](https://msdn.microsoft.com/vs2008/products/cc268305.aspx)

<span data-ttu-id="2af27-136">或者，可以通过 Visual Web Developer Express 2008 创建 ASP.NET MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="2af27-136">Alternatively, you can create ASP.NET MVC applications with Visual Web Developer Express 2008.</span></span> <span data-ttu-id="2af27-137">如果决定使用 Visual Web Developer Express，则必须安装 Service Pack 1。</span><span class="sxs-lookup"><span data-stu-id="2af27-137">If you decide to use Visual Web Developer Express then you must have Service Pack 1 installed.</span></span> <span data-ttu-id="2af27-138">你可以从此网站下载 Visual Web Developer 2008 Express Service Pack 1：</span><span class="sxs-lookup"><span data-stu-id="2af27-138">You can download Visual Web Developer 2008 Express with Service Pack 1 from this website:</span></span>

[<span data-ttu-id="2af27-139">https://www.microsoft.com/downloads/details.aspx?FamilyId=BDB6391C-05CA-4036-9154-6DF4F6DEBD14&amp;d isplaylang = en</span><span class="sxs-lookup"><span data-stu-id="2af27-139">https://www.microsoft.com/downloads/details.aspx?FamilyId=BDB6391C-05CA-4036-9154-6DF4F6DEBD14&amp;displaylang=en</span></span>](https://www.microsoft.com/downloads/details.aspx?FamilyId=BDB6391C-05CA-4036-9154-6DF4F6DEBD14&amp;displaylang=en)

<span data-ttu-id="2af27-140">安装 Visual Studio 2008 或 Visual Web Developer 2008 后，需要安装 ASP.NET MVC 框架。</span><span class="sxs-lookup"><span data-stu-id="2af27-140">After you install either Visual Studio 2008 or Visual Web Developer 2008, you need to install the ASP.NET MVC framework.</span></span> <span data-ttu-id="2af27-141">你可以从以下网站下载 ASP.NET MVC 框架：</span><span class="sxs-lookup"><span data-stu-id="2af27-141">You can download the ASP.NET MVC framework from the following website:</span></span>

[https://www.asp.net/mvc/](../../../index.md)

> [!NOTE] 
> 
> <span data-ttu-id="2af27-142">你可以利用 Web 平台安装程序，而不是单独下载 ASP.NET framework 和 ASP.NET MVC 框架。</span><span class="sxs-lookup"><span data-stu-id="2af27-142">Instead of downloading the ASP.NET framework and the ASP.NET MVC framework individually, you can take advantage of the Web Platform Installer.</span></span> <span data-ttu-id="2af27-143">Web 平台安装程序是一种应用程序，使你能够轻松地管理已安装的应用程序是否为你的计算机：</span><span class="sxs-lookup"><span data-stu-id="2af27-143">The Web Platform Installer is an application that enables you to easily manage the installed applications are your computer:</span></span>
> 
> [https://www.microsoft.com/web/gallery/Install.aspx](https://www.microsoft.com/web/gallery/Install.aspx)

## <a name="creating-an-aspnet-mvc-web-application-project"></a><span data-ttu-id="2af27-144">创建 ASP.NET MVC Web 应用程序项目</span><span class="sxs-lookup"><span data-stu-id="2af27-144">Creating an ASP.NET MVC Web Application Project</span></span>

<span data-ttu-id="2af27-145">首先，让我们在 Visual Studio 2008 中创建新的 ASP.NET MVC Web 应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="2af27-145">Let's start by creating a new ASP.NET MVC Web Application project in Visual Studio 2008.</span></span> <span data-ttu-id="2af27-146">选择菜单选项 "**文件"、"新建项目**"，您将看到图1中的 "新建项目" 对话框。</span><span class="sxs-lookup"><span data-stu-id="2af27-146">Select the menu option **File, New Project** and you will see the New Project dialog box in Figure 1.</span></span> <span data-ttu-id="2af27-147">选择C#作为编程语言，然后选择 "ASP.NET MVC Web 应用程序" 项目模板。</span><span class="sxs-lookup"><span data-stu-id="2af27-147">Select C# as the programming language and select the ASP.NET MVC Web Application project template.</span></span> <span data-ttu-id="2af27-148">为项目指定名称 MovieApp，然后单击 "确定" 按钮。</span><span class="sxs-lookup"><span data-stu-id="2af27-148">Give your project the name MovieApp and click the OK button.</span></span>

<span data-ttu-id="2af27-149">[!["新建项目" 对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image1.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="2af27-149">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image1.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image1.png)</span></span>

<span data-ttu-id="2af27-150">**图 01**： "新建项目" 对话框（[单击以查看完全大小的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="2af27-150">**Figure 01**: The New Project dialog box ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image2.png))</span></span>

<span data-ttu-id="2af27-151">请确保从 "新建项目" 对话框顶部的下拉列表中选择 .NET Framework 3.5，否则不会出现 "ASP.NET MVC Web 应用程序" 项目模板。</span><span class="sxs-lookup"><span data-stu-id="2af27-151">Make sure that you select .NET Framework 3.5 from the dropdown list at the top of the New Project dialog or the ASP.NET MVC Web Application project template won't appear.</span></span>

<span data-ttu-id="2af27-152">每次创建新的 MVC Web 应用程序项目时，Visual Studio 都会提示您创建一个单独的单元测试项目。</span><span class="sxs-lookup"><span data-stu-id="2af27-152">Whenever you create a new MVC Web Application project, Visual Studio prompts you to create a separate unit test project.</span></span> <span data-ttu-id="2af27-153">图2中的对话框随即出现。</span><span class="sxs-lookup"><span data-stu-id="2af27-153">The dialog in Figure 2 appears.</span></span> <span data-ttu-id="2af27-154">由于我们不会在本教程中创建测试，因为存在时间限制（是的，我们应该感觉到投机取巧），请选择 "**否**" 选项，然后单击 **"确定"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="2af27-154">Because we won't be creating tests in this tutorial because of time constraints (and, yes, we should feel a little guilty about this) select the **No** option and click the **OK** button.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="2af27-155">Visual Web Developer 不支持测试项目。</span><span class="sxs-lookup"><span data-stu-id="2af27-155">Visual Web Developer does not support test projects.</span></span>

<span data-ttu-id="2af27-156">[!["新建项目" 对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image2.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="2af27-156">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image2.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image3.png)</span></span>

<span data-ttu-id="2af27-157">**图 02**： "创建单元测试项目" 对话框（[单击以查看完全大小的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image4.png)）</span><span class="sxs-lookup"><span data-stu-id="2af27-157">**Figure 02**: The Create Unit Test Project dialog ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image4.png))</span></span>

<span data-ttu-id="2af27-158">ASP.NET MVC 应用程序具有一组标准文件夹：模型、视图和控制器文件夹。</span><span class="sxs-lookup"><span data-stu-id="2af27-158">An ASP.NET MVC application has a standard set of folders: a Models, Views, and Controllers folder.</span></span> <span data-ttu-id="2af27-159">您可以在 "解决方案资源管理器" 窗口中查看此标准文件夹集。</span><span class="sxs-lookup"><span data-stu-id="2af27-159">You can see this standard set of folders in the Solution Explorer window.</span></span> <span data-ttu-id="2af27-160">为了构建电影数据库应用程序，我们需要将文件添加到每个模型、视图和控制器文件夹中。</span><span class="sxs-lookup"><span data-stu-id="2af27-160">We'll need to add files to each of the Models, Views, and Controllers folders in order to build our Movie Database application.</span></span>

<span data-ttu-id="2af27-161">使用 Visual Studio 创建新的 MVC 应用程序时，将获得一个示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="2af27-161">When you create a new MVC application with Visual Studio, you get a sample application.</span></span> <span data-ttu-id="2af27-162">由于我们要从头开始，我们需要删除此示例应用程序的内容。</span><span class="sxs-lookup"><span data-stu-id="2af27-162">Because we want to start from scratch, we need to delete the content for this sample application.</span></span> <span data-ttu-id="2af27-163">需要删除以下文件和下列文件夹：</span><span class="sxs-lookup"><span data-stu-id="2af27-163">You need to delete the following file and the following folder:</span></span>

- <span data-ttu-id="2af27-164">Controllers\HomeController.cs</span><span class="sxs-lookup"><span data-stu-id="2af27-164">Controllers\HomeController.cs</span></span>
- <span data-ttu-id="2af27-165">Views\Home</span><span class="sxs-lookup"><span data-stu-id="2af27-165">Views\Home</span></span>

## <a name="creating-the-database"></a><span data-ttu-id="2af27-166">创建数据库</span><span class="sxs-lookup"><span data-stu-id="2af27-166">Creating the Database</span></span>

<span data-ttu-id="2af27-167">我们需要创建一个数据库来存放电影数据库记录。</span><span class="sxs-lookup"><span data-stu-id="2af27-167">We need to create a database to hold our movie database records.</span></span> <span data-ttu-id="2af27-168">幸运的是，Visual Studio 包括一个名为 SQL Server Express 的免费数据库。</span><span class="sxs-lookup"><span data-stu-id="2af27-168">Luckily, Visual Studio includes a free database named SQL Server Express.</span></span> <span data-ttu-id="2af27-169">按照以下步骤创建数据库：</span><span class="sxs-lookup"><span data-stu-id="2af27-169">Follow these steps to create the database:</span></span>

1. <span data-ttu-id="2af27-170">右键单击 "解决方案资源管理器" 窗口中的 "应用\_Data" 文件夹，然后选择 "**添加"、"新建项**" 菜单。</span><span class="sxs-lookup"><span data-stu-id="2af27-170">Right-click the App\_Data folder in the Solution Explorer window and select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="2af27-171">选择 "**数据**" 类别，然后选择 " **SQL Server" 数据库**模板（请参阅图3）。</span><span class="sxs-lookup"><span data-stu-id="2af27-171">Select the **Data** category and select the **SQL Server Database** template (see Figure 3).</span></span>
3. <span data-ttu-id="2af27-172">将新数据库命名为*MoviesDB* ，然后单击 "**添加**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="2af27-172">Name your new database *MoviesDB.mdf* and click the **Add** button.</span></span>

<span data-ttu-id="2af27-173">创建数据库后，可以通过双击位于应用\_Data 文件夹中的 MoviesDB 文件来连接到数据库。</span><span class="sxs-lookup"><span data-stu-id="2af27-173">After you create your database, you can connect to the database by double-clicking the MoviesDB.mdf file located in the App\_Data folder.</span></span> <span data-ttu-id="2af27-174">双击 MoviesDB 文件将打开 "服务器资源管理器" 窗口。</span><span class="sxs-lookup"><span data-stu-id="2af27-174">Double-clicking the MoviesDB.mdf file opens the Server Explorer window.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="2af27-175">在 Visual Web Developer 的情况下，"服务器资源管理器" 窗口称为数据库资源管理器 "窗口。</span><span class="sxs-lookup"><span data-stu-id="2af27-175">The Server Explorer window is named the Database Explorer window in the case of Visual Web Developer.</span></span>

<span data-ttu-id="2af27-176">[!["新建项目" 对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image3.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="2af27-176">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image3.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image5.png)</span></span>

<span data-ttu-id="2af27-177">**图 03**：创建 Microsoft SQL Server 数据库（[单击查看完全大小的映像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="2af27-177">**Figure 03**: Creating a Microsoft SQL Server Database ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image6.png))</span></span>

<span data-ttu-id="2af27-178">接下来，需要创建一个新的数据库表。</span><span class="sxs-lookup"><span data-stu-id="2af27-178">Next, we need to create a new database table.</span></span> <span data-ttu-id="2af27-179">从 "服务器资源管理器" 窗口中，右键单击 "表" 文件夹，然后选择菜单选项 "**添加新表**"。</span><span class="sxs-lookup"><span data-stu-id="2af27-179">From within the Sever Explorer window, right-click the Tables folder and select the menu option **Add New Table**.</span></span> <span data-ttu-id="2af27-180">选择此菜单选项将打开数据库表设计器。</span><span class="sxs-lookup"><span data-stu-id="2af27-180">Selecting this menu option opens the database table designer.</span></span> <span data-ttu-id="2af27-181">创建以下数据库列：</span><span class="sxs-lookup"><span data-stu-id="2af27-181">Create the following database columns:</span></span>

<a id="0.1_table01"></a>

| <span data-ttu-id="2af27-182">**列名**</span><span class="sxs-lookup"><span data-stu-id="2af27-182">**Column Name**</span></span> | <span data-ttu-id="2af27-183">**数据类型**</span><span class="sxs-lookup"><span data-stu-id="2af27-183">**Data Type**</span></span> | <span data-ttu-id="2af27-184">**允许空值**</span><span class="sxs-lookup"><span data-stu-id="2af27-184">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2af27-185">Id</span><span class="sxs-lookup"><span data-stu-id="2af27-185">Id</span></span> | <span data-ttu-id="2af27-186">Int</span><span class="sxs-lookup"><span data-stu-id="2af27-186">Int</span></span> | <span data-ttu-id="2af27-187">False</span><span class="sxs-lookup"><span data-stu-id="2af27-187">False</span></span> |
| <span data-ttu-id="2af27-188">职务</span><span class="sxs-lookup"><span data-stu-id="2af27-188">Title</span></span> | <span data-ttu-id="2af27-189">Nvarchar （100）</span><span class="sxs-lookup"><span data-stu-id="2af27-189">Nvarchar(100)</span></span> | <span data-ttu-id="2af27-190">False</span><span class="sxs-lookup"><span data-stu-id="2af27-190">False</span></span> |
| <span data-ttu-id="2af27-191">9509</span><span class="sxs-lookup"><span data-stu-id="2af27-191">Director</span></span> | <span data-ttu-id="2af27-192">Nvarchar （100）</span><span class="sxs-lookup"><span data-stu-id="2af27-192">Nvarchar(100)</span></span> | <span data-ttu-id="2af27-193">False</span><span class="sxs-lookup"><span data-stu-id="2af27-193">False</span></span> |
| <span data-ttu-id="2af27-194">DateReleased</span><span class="sxs-lookup"><span data-stu-id="2af27-194">DateReleased</span></span> | <span data-ttu-id="2af27-195">DateTime</span><span class="sxs-lookup"><span data-stu-id="2af27-195">DateTime</span></span> | <span data-ttu-id="2af27-196">False</span><span class="sxs-lookup"><span data-stu-id="2af27-196">False</span></span> |

<span data-ttu-id="2af27-197">第一列（Id 列）包含两个特殊属性。</span><span class="sxs-lookup"><span data-stu-id="2af27-197">The first column, the Id column, has two special properties.</span></span> <span data-ttu-id="2af27-198">首先，需要将 Id 列标记为主键列。</span><span class="sxs-lookup"><span data-stu-id="2af27-198">First, you need to mark the Id column as the primary key column.</span></span> <span data-ttu-id="2af27-199">选择 Id 列后，单击 "**设置主键**" 按钮（它是看起来像一个键的图标）。</span><span class="sxs-lookup"><span data-stu-id="2af27-199">After selecting the Id column, click the **Set Primary Key** button (it is the icon that looks like a key).</span></span> <span data-ttu-id="2af27-200">其次，需要将 Id 列标记为标识列。</span><span class="sxs-lookup"><span data-stu-id="2af27-200">Second, you need to mark the Id column as an Identity column.</span></span> <span data-ttu-id="2af27-201">在属性窗口列中，向下滚动到 "标识规范" 部分并展开它。</span><span class="sxs-lookup"><span data-stu-id="2af27-201">In the Column Properties window, scroll down to the Identity Specification section and expand it.</span></span> <span data-ttu-id="2af27-202">将 "**是" 标识**属性更改为 **"是"** 。</span><span class="sxs-lookup"><span data-stu-id="2af27-202">Change the **Is Identity** property to the value **Yes**.</span></span> <span data-ttu-id="2af27-203">完成后，表应如图4所示。</span><span class="sxs-lookup"><span data-stu-id="2af27-203">When you are finished, the table should look like Figure 4.</span></span>

<span data-ttu-id="2af27-204">[!["新建项目" 对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image4.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="2af27-204">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image4.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image7.png)</span></span>

<span data-ttu-id="2af27-205">**图 04**：电影数据库表（[单击以查看完全大小的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image8.png)）</span><span class="sxs-lookup"><span data-stu-id="2af27-205">**Figure 04**: The Movies database table ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image8.png))</span></span>

<span data-ttu-id="2af27-206">最后一步是保存新表。</span><span class="sxs-lookup"><span data-stu-id="2af27-206">The final step is to save the new table.</span></span> <span data-ttu-id="2af27-207">单击 "保存" 按钮（软盘的图标），并为新表命名为 "电影"。</span><span class="sxs-lookup"><span data-stu-id="2af27-207">Click the Save button (the icon of the floppy) and give the new table the name Movies.</span></span>

<span data-ttu-id="2af27-208">创建完表后，将一些电影记录添加到表中。</span><span class="sxs-lookup"><span data-stu-id="2af27-208">After you finish creating the table, add some movie records to the table.</span></span> <span data-ttu-id="2af27-209">右键单击 "服务器资源管理器" 窗口中的 "电影" 表，然后选择菜单选项 "**显示表数据**"。</span><span class="sxs-lookup"><span data-stu-id="2af27-209">Right-click the Movies table in the Server Explorer window and select the menu option **Show Table Data**.</span></span> <span data-ttu-id="2af27-210">输入喜欢的电影列表（见图5）。</span><span class="sxs-lookup"><span data-stu-id="2af27-210">Enter a list of your favorite movies (see Figure 5).</span></span>

<span data-ttu-id="2af27-211">[!["新建项目" 对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image5.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="2af27-211">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image5.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image9.png)</span></span>

<span data-ttu-id="2af27-212">**图 05**：输入电影记录（[单击以查看完全大小的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image10.png)）</span><span class="sxs-lookup"><span data-stu-id="2af27-212">**Figure 05**: Entering movie records ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image10.png))</span></span>

## <a name="creating-the-model"></a><span data-ttu-id="2af27-213">创建模型</span><span class="sxs-lookup"><span data-stu-id="2af27-213">Creating the Model</span></span>

<span data-ttu-id="2af27-214">接下来，需要创建一组类以表示数据库。</span><span class="sxs-lookup"><span data-stu-id="2af27-214">We next need to create a set of classes to represent our database.</span></span> <span data-ttu-id="2af27-215">我们需要创建一个数据库模型。</span><span class="sxs-lookup"><span data-stu-id="2af27-215">We need to create a database model.</span></span> <span data-ttu-id="2af27-216">我们将利用 Microsoft 实体框架自动为数据库模型生成类。</span><span class="sxs-lookup"><span data-stu-id="2af27-216">We'll take advantage of the Microsoft Entity Framework to generate the classes for our database model automatically.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="2af27-217">ASP.NET MVC 框架不与 Microsoft 实体框架相关联。</span><span class="sxs-lookup"><span data-stu-id="2af27-217">The ASP.NET MVC framework is not tied to the Microsoft Entity Framework.</span></span> <span data-ttu-id="2af27-218">可以通过利用各种对象关系映射（或/M）工具（包括 LINQ to SQL、Subsonic 和 NHibernate）来创建数据库模型类。</span><span class="sxs-lookup"><span data-stu-id="2af27-218">You can create your database model classes by taking advantage of a variety of Object Relational Mapping (OR/M) tools including LINQ to SQL, Subsonic, and NHibernate.</span></span>

<span data-ttu-id="2af27-219">请按照以下步骤启动实体数据模型向导：</span><span class="sxs-lookup"><span data-stu-id="2af27-219">Follow these steps to launch the Entity Data Model Wizard:</span></span>

1. <span data-ttu-id="2af27-220">右键单击 "解决方案资源管理器" 窗口中的 "模型" 文件夹，然后选择 "**添加"、"新建项**" 菜单。</span><span class="sxs-lookup"><span data-stu-id="2af27-220">Right-click the Models folder in the Solution Explorer window and the select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="2af27-221">选择 "**数据**" 类别，然后选择 " **ADO.NET 实体数据模型**" 模板。</span><span class="sxs-lookup"><span data-stu-id="2af27-221">Select the **Data** category and select the **ADO.NET Entity Data Model** template.</span></span>
3. <span data-ttu-id="2af27-222">为数据模型指定名称*MoviesDBModel* ，并单击 "**添加**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="2af27-222">Give your data model the name *MoviesDBModel.edmx* and click the **Add** button.</span></span>

<span data-ttu-id="2af27-223">单击 "添加" 按钮后，将显示 "实体数据模型" 向导（见图6）。</span><span class="sxs-lookup"><span data-stu-id="2af27-223">After you click the Add button, the Entity Data Model Wizard appears (see Figure 6).</span></span> <span data-ttu-id="2af27-224">按照以下步骤完成向导：</span><span class="sxs-lookup"><span data-stu-id="2af27-224">Follow these steps to complete the wizard:</span></span>

1. <span data-ttu-id="2af27-225">在 "**选择模型内容**" 步骤中，选择 "**从数据库生成**" 选项。</span><span class="sxs-lookup"><span data-stu-id="2af27-225">In the **Choose Model Contents** step, select the **Generate from database** option.</span></span>
2. <span data-ttu-id="2af27-226">在 "**选择你的数据连接**" 步骤中，使用*MoviesDB*数据连接，并为连接设置使用名称 " *MoviesDBEntities* "。</span><span class="sxs-lookup"><span data-stu-id="2af27-226">In the **Choose Your Data Connection** step, use the *MoviesDB.mdf* data connection and the name *MoviesDBEntities* for the connection settings.</span></span> <span data-ttu-id="2af27-227">单击 "**下一步**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="2af27-227">Click the **Next** button.</span></span>
3. <span data-ttu-id="2af27-228">在 "**选择数据库对象**" 步骤中，展开 "表" 节点，然后选择 "电影" 表。</span><span class="sxs-lookup"><span data-stu-id="2af27-228">In the **Choose Your Database Objects** step, expand the Tables node, select the Movies table.</span></span> <span data-ttu-id="2af27-229">输入命名空间*MovieApp* ，并单击 "**完成**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="2af27-229">Enter the namespace *MovieApp.Models* and click the **Finish** button.</span></span>

<span data-ttu-id="2af27-230">[!["新建项目" 对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image6.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="2af27-230">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image6.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image11.png)</span></span>

<span data-ttu-id="2af27-231">**图 06**：使用实体数据模型向导生成数据库模型（[单击以查看完全大小的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image12.png)）</span><span class="sxs-lookup"><span data-stu-id="2af27-231">**Figure 06**: Generating a database model with the Entity Data Model Wizard ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image12.png))</span></span>

<span data-ttu-id="2af27-232">完成实体数据模型向导后，"实体数据模型设计器会打开。</span><span class="sxs-lookup"><span data-stu-id="2af27-232">After you complete the Entity Data Model Wizard, the Entity Data Model Designer opens.</span></span> <span data-ttu-id="2af27-233">设计器应显示电影数据库表（参见图7）。</span><span class="sxs-lookup"><span data-stu-id="2af27-233">The Designer should display the Movies database table (see Figure 7).</span></span>

<span data-ttu-id="2af27-234">[!["新建项目" 对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image7.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="2af27-234">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image7.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image13.png)</span></span>

<span data-ttu-id="2af27-235">**图 07**：实体数据模型设计器（[单击查看完全尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image14.png)）</span><span class="sxs-lookup"><span data-stu-id="2af27-235">**Figure 07**: The Entity Data Model Designer ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image14.png))</span></span>

<span data-ttu-id="2af27-236">在继续操作之前，我们需要进行一项更改。</span><span class="sxs-lookup"><span data-stu-id="2af27-236">We need to make one change before we continue.</span></span> <span data-ttu-id="2af27-237">实体数据向导将生成一个名为*电影*的模型类，该类表示电影数据库表。</span><span class="sxs-lookup"><span data-stu-id="2af27-237">The Entity Data Wizard generates a model class named *Movies* that represents the Movies database table.</span></span> <span data-ttu-id="2af27-238">由于我们将使用 movie 类来表示特定电影，因此我们需要将类的名称修改为*电影*，而不是*影片*（单数形式）。</span><span class="sxs-lookup"><span data-stu-id="2af27-238">Because we'll use the Movies class to represent a particular movie, we need to modify the name of the class to be *Movie* instead of *Movies* (singular rather than plural).</span></span>

<span data-ttu-id="2af27-239">双击设计器图面上类的名称，并将类的名称从 "电影" 更改为 "电影"。</span><span class="sxs-lookup"><span data-stu-id="2af27-239">Double-click the name of the class on the designer surface and change the name of the class from Movies to Movie.</span></span> <span data-ttu-id="2af27-240">做出此更改后，单击 "**保存**" 按钮（软盘的图标）以生成 Movie 类。</span><span class="sxs-lookup"><span data-stu-id="2af27-240">After making this change, click the **Save** button (the icon of the floppy disk) to generate the Movie class.</span></span>

## <a name="creating-the-aspnet-mvc-controller"></a><span data-ttu-id="2af27-241">创建 ASP.NET MVC 控制器</span><span class="sxs-lookup"><span data-stu-id="2af27-241">Creating the ASP.NET MVC Controller</span></span>

<span data-ttu-id="2af27-242">下一步是创建 ASP.NET MVC 控制器。</span><span class="sxs-lookup"><span data-stu-id="2af27-242">The next step is to create the ASP.NET MVC controller.</span></span> <span data-ttu-id="2af27-243">控制器负责控制用户如何与 ASP.NET MVC 应用程序交互。</span><span class="sxs-lookup"><span data-stu-id="2af27-243">A controller is responsible for controlling how a user interacts with an ASP.NET MVC application.</span></span>

<span data-ttu-id="2af27-244">按照以下步骤进行操作：</span><span class="sxs-lookup"><span data-stu-id="2af27-244">Follow these steps:</span></span>

1. <span data-ttu-id="2af27-245">在 "解决方案资源管理器" 窗口中，右键单击 "控制器" 文件夹，然后选择 "**添加"、"控制器**" 菜单。</span><span class="sxs-lookup"><span data-stu-id="2af27-245">In the Solution Explorer window, right-click the Controllers folder and select the menu option **Add, Controller**.</span></span>
2. <span data-ttu-id="2af27-246">在 "添加控制器" 对话框中，输入名称*HomeController* ，并选中标签为 "**添加" "创建"、"更新" 和 "详细信息" 方案的 "操作方法**" 的复选框（见图8）</span><span class="sxs-lookup"><span data-stu-id="2af27-246">In the Add Controller dialog, enter the name *HomeController* and check the checkbox labeled **Add action methods for Create, Update, and Details scenarios** (see Figure 8).</span></span>
3. <span data-ttu-id="2af27-247">单击 "**添加**" 按钮将新的控制器添加到项目。</span><span class="sxs-lookup"><span data-stu-id="2af27-247">Click the **Add** button to add the new controller to your project.</span></span>

<span data-ttu-id="2af27-248">完成这些步骤后，会创建列表1中的控制器。</span><span class="sxs-lookup"><span data-stu-id="2af27-248">After you complete these steps, the controller in Listing 1 is created.</span></span> <span data-ttu-id="2af27-249">请注意，它包含名为索引、详细信息、创建和编辑的方法。</span><span class="sxs-lookup"><span data-stu-id="2af27-249">Notice that it contains methods named Index, Details, Create, and Edit.</span></span> <span data-ttu-id="2af27-250">在以下部分中，我们将添加所需的代码以使这些方法正常工作。</span><span class="sxs-lookup"><span data-stu-id="2af27-250">In the following sections, we'll add the necessary code to get these methods to work.</span></span>

<span data-ttu-id="2af27-251">[!["新建项目" 对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image8.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="2af27-251">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image8.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image15.png)</span></span>

<span data-ttu-id="2af27-252">**图 08**：添加新的 ASP.NET MVC 控制器（[单击以查看完全大小的映像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image16.png)）</span><span class="sxs-lookup"><span data-stu-id="2af27-252">**Figure 08**: Adding a new ASP.NET MVC Controller ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image16.png))</span></span>

<span data-ttu-id="2af27-253">**列表1– Controllers\HomeController.cs**</span><span class="sxs-lookup"><span data-stu-id="2af27-253">**Listing 1 – Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/samples/sample1.cs)]

## <a name="listing-database-records"></a><span data-ttu-id="2af27-254">列出数据库记录</span><span class="sxs-lookup"><span data-stu-id="2af27-254">Listing Database Records</span></span>

<span data-ttu-id="2af27-255">Home 控制器的 Index （）方法是 ASP.NET MVC 应用程序的默认方法。</span><span class="sxs-lookup"><span data-stu-id="2af27-255">The Index() method of the Home controller is the default method for an ASP.NET MVC application.</span></span> <span data-ttu-id="2af27-256">运行 ASP.NET MVC 应用程序时，Index （）方法是调用的第一个控制器方法。</span><span class="sxs-lookup"><span data-stu-id="2af27-256">When you run an ASP.NET MVC application, the Index() method is the first controller method that is called.</span></span>

<span data-ttu-id="2af27-257">我们将使用 Index （）方法显示电影数据库表中的记录列表。</span><span class="sxs-lookup"><span data-stu-id="2af27-257">We'll use the Index() method to display the list of records from the Movies database table.</span></span> <span data-ttu-id="2af27-258">我们将利用之前创建的数据库模型类，通过 Index （）方法检索电影数据库记录。</span><span class="sxs-lookup"><span data-stu-id="2af27-258">We'll take advantage of the database model classes that we created earlier to retrieve the movie database records with the Index() method.</span></span>

<span data-ttu-id="2af27-259">我修改了清单2中的 HomeController 类，使其包含一个名为 \_db 的新私有字段。</span><span class="sxs-lookup"><span data-stu-id="2af27-259">I've modified the HomeController class in Listing 2 so that it contains a new private field named \_db.</span></span> <span data-ttu-id="2af27-260">MoviesDBEntities 类表示我们的数据库模型，我们将使用此类与数据库进行通信。</span><span class="sxs-lookup"><span data-stu-id="2af27-260">The MoviesDBEntities class represents our database model and we'll use this class to communicate with our database.</span></span>

<span data-ttu-id="2af27-261">我还在清单2中修改了 Index （）方法。</span><span class="sxs-lookup"><span data-stu-id="2af27-261">I've also modified the Index() method in Listing 2.</span></span> <span data-ttu-id="2af27-262">Index （）方法使用 MoviesDBEntities 类来检索电影数据库表中的所有电影记录。</span><span class="sxs-lookup"><span data-stu-id="2af27-262">The Index() method uses the MoviesDBEntities class to retrieve all of the movie records from the Movies database table.</span></span> <span data-ttu-id="2af27-263">表达式 *\_db。MovieSet. System.linq.enumerable.tolist （）* 返回电影数据库表中所有电影记录的列表。</span><span class="sxs-lookup"><span data-stu-id="2af27-263">The expression *\_db.MovieSet.ToList()* returns a list of all of the movie records from the Movies database table.</span></span>

<span data-ttu-id="2af27-264">电影列表将传递给视图。</span><span class="sxs-lookup"><span data-stu-id="2af27-264">The list of movies is passed to the view.</span></span> <span data-ttu-id="2af27-265">传递给 View （）方法的任何内容都将作为视图数据传递给视图。</span><span class="sxs-lookup"><span data-stu-id="2af27-265">Anything that gets passed to the View() method gets passed to the view as view data.</span></span>

<span data-ttu-id="2af27-266">**列出2–控制器/HomeController （修改的索引方法）**</span><span class="sxs-lookup"><span data-stu-id="2af27-266">**Listing 2 – Controllers/HomeController.cs (modified Index method)**</span></span>

[!code-csharp[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/samples/sample2.cs)]

<span data-ttu-id="2af27-267">Index （）方法返回一个名为 Index 的视图。</span><span class="sxs-lookup"><span data-stu-id="2af27-267">The Index() method returns a view named Index.</span></span> <span data-ttu-id="2af27-268">需要创建此视图来显示电影数据库记录的列表。</span><span class="sxs-lookup"><span data-stu-id="2af27-268">We need to create this view to display the list of movie database records.</span></span> <span data-ttu-id="2af27-269">按照以下步骤进行操作：</span><span class="sxs-lookup"><span data-stu-id="2af27-269">Follow these steps:</span></span>

<span data-ttu-id="2af27-270">在打开 "**添加视图**" 对话框或在 "**查看数据类**" 下拉列表中未显示任何类之前，应生成项目（选择菜单选项 "**生成"、"生成解决方案**"）。</span><span class="sxs-lookup"><span data-stu-id="2af27-270">You should build your project (select the menu option **Build, Build Solution**) before opening the **Add View** dialog or no classes will appear in the **View data class** dropdown list.</span></span>

1. <span data-ttu-id="2af27-271">在代码编辑器中右键单击 Index （）方法，然后选择菜单选项 "**添加视图**" （参见图9）。</span><span class="sxs-lookup"><span data-stu-id="2af27-271">Right-click the Index() method in the code editor and select the menu option **Add View** (see Figure 9).</span></span>
2. <span data-ttu-id="2af27-272">在 "添加视图" 对话框中，验证是否选中了标记为 "**创建强类型视图**" 的复选框。</span><span class="sxs-lookup"><span data-stu-id="2af27-272">In the Add View dialog, verify that the checkbox labeled **Create a strongly-typed view** is checked.</span></span>
3. <span data-ttu-id="2af27-273">从 "**查看内容**" 下拉列表中，选择 "值"*列表*。</span><span class="sxs-lookup"><span data-stu-id="2af27-273">From the **View content** dropdown list, select the value *List*.</span></span>
4. <span data-ttu-id="2af27-274">从 "**查看数据类**" 下拉列表中，选择值*MovieApp*。</span><span class="sxs-lookup"><span data-stu-id="2af27-274">From the **View data class** dropdown list, select the value *MovieApp.Models.Movie*.</span></span>
5. <span data-ttu-id="2af27-275">单击 "添加" 按钮创建新视图（请参阅图10）。</span><span class="sxs-lookup"><span data-stu-id="2af27-275">Click the Add button to create the new view (see Figure 10).</span></span>

<span data-ttu-id="2af27-276">完成这些步骤后，会将名为 "Views\Home" 的新视图添加到 "" 文件夹。</span><span class="sxs-lookup"><span data-stu-id="2af27-276">After you complete these steps, a new view named Index.aspx is added to the Views\Home folder.</span></span> <span data-ttu-id="2af27-277">索引视图的内容包括在列表3中。</span><span class="sxs-lookup"><span data-stu-id="2af27-277">The contents of the Index view are included in Listing 3.</span></span>

<span data-ttu-id="2af27-278">[!["新建项目" 对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image9.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="2af27-278">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image9.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image17.png)</span></span>

<span data-ttu-id="2af27-279">**图 09**：通过控制器操作添加视图（[单击查看完全大小的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image18.png)）</span><span class="sxs-lookup"><span data-stu-id="2af27-279">**Figure 09**: Adding a view from a controller action ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image18.png))</span></span>

<span data-ttu-id="2af27-280">[!["新建项目" 对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image10.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="2af27-280">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image10.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image19.png)</span></span>

<span data-ttu-id="2af27-281">**图 10**：使用 "添加视图" 对话框创建新视图（[单击查看完全尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image20.png)）</span><span class="sxs-lookup"><span data-stu-id="2af27-281">**Figure 10**: Creating a new view with the Add View dialog ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image20.png))</span></span>

<span data-ttu-id="2af27-282">**列表 3-Views\Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="2af27-282">**Listing 3 – Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/samples/sample3.aspx)]

<span data-ttu-id="2af27-283">"索引" 视图显示 HTML 表中电影数据库表的所有电影记录。</span><span class="sxs-lookup"><span data-stu-id="2af27-283">The Index view displays all of the movie records from the Movies database table within an HTML table.</span></span> <span data-ttu-id="2af27-284">视图包含一个 foreach 循环，该循环可循环访问 ViewData 属性所表示的每个电影。</span><span class="sxs-lookup"><span data-stu-id="2af27-284">The view contains a foreach loop that iterates through each movie represented by the ViewData.Model property.</span></span> <span data-ttu-id="2af27-285">如果通过按 F5 键运行应用程序，则会看到图11中的网页。</span><span class="sxs-lookup"><span data-stu-id="2af27-285">If you run your application by hitting the F5 key, then you'll see the web page in Figure 11.</span></span>

<span data-ttu-id="2af27-286">[!["新建项目" 对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image11.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="2af27-286">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image11.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image21.png)</span></span>

<span data-ttu-id="2af27-287">**图 11**： "索引" 视图（[单击以查看完全大小的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image22.png)）</span><span class="sxs-lookup"><span data-stu-id="2af27-287">**Figure 11**: The Index view ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image22.png))</span></span>

## <a name="creating-new-database-records"></a><span data-ttu-id="2af27-288">创建新的数据库记录</span><span class="sxs-lookup"><span data-stu-id="2af27-288">Creating New Database Records</span></span>

<span data-ttu-id="2af27-289">在上一部分中创建的 "索引" 视图包含用于创建新数据库记录的链接。</span><span class="sxs-lookup"><span data-stu-id="2af27-289">The Index view that we created in the previous section includes a link for creating new database records.</span></span> <span data-ttu-id="2af27-290">接下来，实现逻辑，并创建创建新的电影数据库记录所需的视图。</span><span class="sxs-lookup"><span data-stu-id="2af27-290">Let's go ahead and implement the logic and create the view necessary for creating new movie database records.</span></span>

<span data-ttu-id="2af27-291">Home 控制器包含两个名为 Create （）的方法。</span><span class="sxs-lookup"><span data-stu-id="2af27-291">The Home controller contains two methods named Create().</span></span> <span data-ttu-id="2af27-292">第一个 Create （）方法没有参数。</span><span class="sxs-lookup"><span data-stu-id="2af27-292">The first Create() method has no parameters.</span></span> <span data-ttu-id="2af27-293">Create （）方法的此重载用于显示用于创建新的电影数据库记录的 HTML 窗体。</span><span class="sxs-lookup"><span data-stu-id="2af27-293">This overload of the Create() method is used to display the HTML form for creating a new movie database record.</span></span>

<span data-ttu-id="2af27-294">第二个 Create （）方法具有 FormCollection 参数。</span><span class="sxs-lookup"><span data-stu-id="2af27-294">The second Create() method has a FormCollection parameter.</span></span> <span data-ttu-id="2af27-295">在将用于创建新电影的 HTML 表单发送到服务器时，将调用 Create （）方法的此重载。</span><span class="sxs-lookup"><span data-stu-id="2af27-295">This overload of the Create() method is called when the HTML form for creating a new movie is posted to the server.</span></span> <span data-ttu-id="2af27-296">请注意，第二个 Create （）方法具有 AcceptVerbs 属性，该属性阻止调用方法，除非执行 HTTP POST 操作。</span><span class="sxs-lookup"><span data-stu-id="2af27-296">Notice that this second Create() method has an AcceptVerbs attribute that prevents the method from being called unless an HTTP POST operation is performed.</span></span>

<span data-ttu-id="2af27-297">此第二个 Create （）方法已在清单4的更新的 HomeController 类中进行了修改。</span><span class="sxs-lookup"><span data-stu-id="2af27-297">This second Create() method has been modified in the updated HomeController class in Listing 4.</span></span> <span data-ttu-id="2af27-298">新版本的 Create （）方法接受 Movie 参数，并包含用于将新电影插入到电影数据库表的逻辑。</span><span class="sxs-lookup"><span data-stu-id="2af27-298">The new version of the Create() method accepts a Movie parameter and contains the logic for inserting a new movie into the Movies database table.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="2af27-299">请注意 "绑定" 属性。</span><span class="sxs-lookup"><span data-stu-id="2af27-299">Notice the Bind attribute.</span></span> <span data-ttu-id="2af27-300">由于我们不想更新 HTML 格式的电影 Id 属性，因此需要显式排除此属性。</span><span class="sxs-lookup"><span data-stu-id="2af27-300">Because we don't want to update the Movie Id property from HTML form, we need to explicitly exclude this property.</span></span>

<span data-ttu-id="2af27-301">**列表4– Controllers\HomeController.cs （已修改的 Create 方法）**</span><span class="sxs-lookup"><span data-stu-id="2af27-301">**Listing 4 – Controllers\HomeController.cs (modified Create method)**</span></span>

[!code-csharp[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/samples/sample4.cs)]

<span data-ttu-id="2af27-302">使用 Visual Studio 可以轻松地创建新的电影数据库记录（见图12）。</span><span class="sxs-lookup"><span data-stu-id="2af27-302">Visual Studio makes it easy to create the form for creating a new movie database record (see Figure 12).</span></span> <span data-ttu-id="2af27-303">按照以下步骤进行操作：</span><span class="sxs-lookup"><span data-stu-id="2af27-303">Follow these steps:</span></span>

1. <span data-ttu-id="2af27-304">在代码编辑器中右键单击 Create （）方法，然后选择菜单选项 "**添加视图**"。</span><span class="sxs-lookup"><span data-stu-id="2af27-304">Right-click the Create() method in the code editor and select the menu option **Add View**.</span></span>
2. <span data-ttu-id="2af27-305">验证标记为 "**创建强类型视图**" 的复选框。</span><span class="sxs-lookup"><span data-stu-id="2af27-305">Verify that the checkbox labeled **Create a strongly-typed view** is checked.</span></span>
3. <span data-ttu-id="2af27-306">从 "**查看内容**" 下拉列表中，选择 "值" "*创建*"。</span><span class="sxs-lookup"><span data-stu-id="2af27-306">From the **View content** dropdown list, select the value *Create*.</span></span>
4. <span data-ttu-id="2af27-307">从 "**查看数据类**" 下拉列表中，选择值*MovieApp*。</span><span class="sxs-lookup"><span data-stu-id="2af27-307">From the **View data class** dropdown list, select the value *MovieApp.Models.Movie*.</span></span>
5. <span data-ttu-id="2af27-308">单击 "**添加**" 按钮创建新视图。</span><span class="sxs-lookup"><span data-stu-id="2af27-308">Click the **Add** button to create the new view.</span></span>

<span data-ttu-id="2af27-309">[!["新建项目" 对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image12.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image23.png)</span><span class="sxs-lookup"><span data-stu-id="2af27-309">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image12.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image23.png)</span></span>

<span data-ttu-id="2af27-310">**图 12**：添加 "创建" 视图（[单击以查看完全大小的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image24.png)）</span><span class="sxs-lookup"><span data-stu-id="2af27-310">**Figure 12**: Adding the Create view ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image24.png))</span></span>

<span data-ttu-id="2af27-311">Visual Studio 会自动生成列表5中的视图。</span><span class="sxs-lookup"><span data-stu-id="2af27-311">Visual Studio generates the view in Listing 5 automatically.</span></span> <span data-ttu-id="2af27-312">此视图包含一个 HTML 窗体，其中包含与 Movie 类的每个属性对应的字段。</span><span class="sxs-lookup"><span data-stu-id="2af27-312">This view contains an HTML form that includes fields that correspond to each of the properties of the Movie class.</span></span>

<span data-ttu-id="2af27-313">**列表5– Views\Home\Create.aspx**</span><span class="sxs-lookup"><span data-stu-id="2af27-313">**Listing 5 – Views\Home\Create.aspx**</span></span>

[!code-aspx[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/samples/sample5.aspx)]

> [!NOTE] 
> 
> <span data-ttu-id="2af27-314">"添加视图" 对话框生成的 HTML 窗体将生成一个 Id 窗体字段。</span><span class="sxs-lookup"><span data-stu-id="2af27-314">The HTML form generated by the Add View dialog generates an Id form field.</span></span> <span data-ttu-id="2af27-315">由于 Id 列是标识列，因此不需要此窗体字段，你可以安全地将其删除。</span><span class="sxs-lookup"><span data-stu-id="2af27-315">Because the Id column is an Identity column, we don't need this form field and you can safely remove it.</span></span>

<span data-ttu-id="2af27-316">添加 "创建" 视图后，可以将新的电影记录添加到数据库中。</span><span class="sxs-lookup"><span data-stu-id="2af27-316">After you add the Create view, you can add new Movie records to the database.</span></span> <span data-ttu-id="2af27-317">按 F5 键运行应用程序，并单击 "新建" 链接以查看图13中的窗体。</span><span class="sxs-lookup"><span data-stu-id="2af27-317">Run your application by pressing the F5 key and click the Create New link to see the form in Figure 13.</span></span> <span data-ttu-id="2af27-318">如果完成并提交了窗体，则将创建一个新的电影数据库记录。</span><span class="sxs-lookup"><span data-stu-id="2af27-318">If you complete and submit the form, a new movie database record is created.</span></span>

<span data-ttu-id="2af27-319">请注意，会自动获得窗体验证。</span><span class="sxs-lookup"><span data-stu-id="2af27-319">Notice that you get form validation automatically.</span></span> <span data-ttu-id="2af27-320">如果您忘记为电影输入发布日期或输入无效的发布日期，则会重新显示窗体，并突出显示 "发布日期" 字段。</span><span class="sxs-lookup"><span data-stu-id="2af27-320">If you neglect to enter a release date for a movie, or you enter an invalid release date, then the form is redisplayed and the release date field is highlighted.</span></span>

<span data-ttu-id="2af27-321">[!["新建项目" 对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image13.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="2af27-321">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image13.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image25.png)</span></span>

<span data-ttu-id="2af27-322">**图 13**：创建新的电影数据库记录（[单击以查看完全大小的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image26.png)）</span><span class="sxs-lookup"><span data-stu-id="2af27-322">**Figure 13**: Creating a new movie database record ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image26.png))</span></span>

## <a name="editing-existing-database-records"></a><span data-ttu-id="2af27-323">编辑现有的数据库记录</span><span class="sxs-lookup"><span data-stu-id="2af27-323">Editing Existing Database Records</span></span>

<span data-ttu-id="2af27-324">在前面的部分中，我们讨论了如何列出和创建新的数据库记录。</span><span class="sxs-lookup"><span data-stu-id="2af27-324">In the previous sections, we discussed how you can list and create new database records.</span></span> <span data-ttu-id="2af27-325">在此最后一节中，我们将讨论如何编辑现有的数据库记录。</span><span class="sxs-lookup"><span data-stu-id="2af27-325">In this final section, we discuss how you can edit existing database records.</span></span>

<span data-ttu-id="2af27-326">首先，我们需要生成编辑窗体。</span><span class="sxs-lookup"><span data-stu-id="2af27-326">First, we need to generate the Edit form.</span></span> <span data-ttu-id="2af27-327">此步骤很简单，因为 Visual Studio 会自动为我们生成编辑窗体。</span><span class="sxs-lookup"><span data-stu-id="2af27-327">This step is easy since Visual Studio will generate the Edit form for us automatically.</span></span> <span data-ttu-id="2af27-328">在 Visual Studio 代码编辑器中打开 HomeController.cs 类，然后执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="2af27-328">Open the HomeController.cs class in the Visual Studio code editor and follow these steps:</span></span>

1. <span data-ttu-id="2af27-329">右键单击代码编辑器中的 Edit （）方法，然后选择 "**添加视图**" 菜单选项（见图14）。</span><span class="sxs-lookup"><span data-stu-id="2af27-329">Right-click the Edit() method in the code editor and select the menu option **Add View** (see Figure 14).</span></span>
2. <span data-ttu-id="2af27-330">选中标签为 "**创建强类型视图**" 的复选框。</span><span class="sxs-lookup"><span data-stu-id="2af27-330">Check the checkbox labeled **Create a strongly-typed view**.</span></span>
3. <span data-ttu-id="2af27-331">从 "**查看内容**" 下拉列表中，选择 "值" "*编辑*"。</span><span class="sxs-lookup"><span data-stu-id="2af27-331">From the **View content** dropdown list, select the value *Edit*.</span></span>
4. <span data-ttu-id="2af27-332">从 "**查看数据类**" 下拉列表中，选择值*MovieApp*。</span><span class="sxs-lookup"><span data-stu-id="2af27-332">From the **View data class** dropdown list, select the value *MovieApp.Models.Movie*.</span></span>
5. <span data-ttu-id="2af27-333">单击 "**添加**" 按钮创建新视图。</span><span class="sxs-lookup"><span data-stu-id="2af27-333">Click the **Add** button to create the new view.</span></span>

<span data-ttu-id="2af27-334">完成这些步骤后，会将名为 "Views\Home" 的新视图添加到 "" 文件夹。</span><span class="sxs-lookup"><span data-stu-id="2af27-334">Completing these steps adds a new view named Edit.aspx to the Views\Home folder.</span></span> <span data-ttu-id="2af27-335">此视图包含用于编辑电影记录的 HTML 窗体。</span><span class="sxs-lookup"><span data-stu-id="2af27-335">This view contains an HTML form for editing a movie record.</span></span>

<span data-ttu-id="2af27-336">[!["新建项目" 对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image14.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image27.png)</span><span class="sxs-lookup"><span data-stu-id="2af27-336">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image14.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image27.png)</span></span>

<span data-ttu-id="2af27-337">**图 14**：添加编辑视图（[单击以查看完全大小的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image28.png)）</span><span class="sxs-lookup"><span data-stu-id="2af27-337">**Figure 14**: Adding the Edit view ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image28.png))</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="2af27-338">编辑视图包含与 "电影 Id" 属性相对应的 HTML 表单域。</span><span class="sxs-lookup"><span data-stu-id="2af27-338">The Edit view contains an HTML form field that corresponds to the Movie Id property.</span></span> <span data-ttu-id="2af27-339">由于不希望用户编辑 Id 属性的值，因此应删除此窗体字段。</span><span class="sxs-lookup"><span data-stu-id="2af27-339">Because you don't want people editing the value of the Id property, you should remove this form field.</span></span>

<span data-ttu-id="2af27-340">最后，我们需要修改 Home 控制器，使其支持编辑数据库记录。</span><span class="sxs-lookup"><span data-stu-id="2af27-340">Finally, we need to modify the Home controller so that it supports editing a database record.</span></span> <span data-ttu-id="2af27-341">已更新的 HomeController 类包含在列表6中。</span><span class="sxs-lookup"><span data-stu-id="2af27-341">The updated HomeController class is contained in Listing 6.</span></span>

<span data-ttu-id="2af27-342">**清单6– Controllers\HomeController.cs （编辑方法）**</span><span class="sxs-lookup"><span data-stu-id="2af27-342">**Listing 6 – Controllers\HomeController.cs (Edit methods)**</span></span>

[!code-csharp[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/samples/sample6.cs)]

<span data-ttu-id="2af27-343">在列表6中，我已将其他逻辑添加到了 Edit （）方法的两个重载。</span><span class="sxs-lookup"><span data-stu-id="2af27-343">In Listing 6, I've added additional logic to both overloads of the Edit() method.</span></span> <span data-ttu-id="2af27-344">第一个 Edit （）方法返回与传递给该方法的 Id 参数相对应的电影数据库记录。</span><span class="sxs-lookup"><span data-stu-id="2af27-344">The first Edit() method returns the movie database record that corresponds to the Id parameter passed to the method.</span></span> <span data-ttu-id="2af27-345">第二个重载对数据库中的电影记录执行更新。</span><span class="sxs-lookup"><span data-stu-id="2af27-345">The second overload performs the updates to a movie record in the database.</span></span>

<span data-ttu-id="2af27-346">请注意，必须检索原始电影，然后调用 ApplyPropertyChanges （）来更新数据库中的现有电影。</span><span class="sxs-lookup"><span data-stu-id="2af27-346">Notice that you must retrieve the original movie, and then call ApplyPropertyChanges(), to update the existing movie in the database.</span></span>

## <a name="summary"></a><span data-ttu-id="2af27-347">总结</span><span class="sxs-lookup"><span data-stu-id="2af27-347">Summary</span></span>

<span data-ttu-id="2af27-348">本教程的目的是让你了解构建 ASP.NET MVC 应用程序的体验。</span><span class="sxs-lookup"><span data-stu-id="2af27-348">The purpose of this tutorial was to give you a sense of the experience of building an ASP.NET MVC application.</span></span> <span data-ttu-id="2af27-349">我希望您发现生成 ASP.NET MVC web 应用程序的过程与生成 Active Server Pages 或 ASP.NET 应用程序的体验非常类似。</span><span class="sxs-lookup"><span data-stu-id="2af27-349">I hope that you discovered that building an ASP.NET MVC web application is very similar to the experience of building an Active Server Pages or ASP.NET application.</span></span>

<span data-ttu-id="2af27-350">在本教程中，我们仅检查了 ASP.NET MVC 框架的最基本功能。</span><span class="sxs-lookup"><span data-stu-id="2af27-350">In this tutorial, we examined only the most basic features of the ASP.NET MVC framework.</span></span> <span data-ttu-id="2af27-351">在将来的教程中，我们将深入探讨控制器、控制器操作、视图、视图数据和 HTML 帮助器等主题。</span><span class="sxs-lookup"><span data-stu-id="2af27-351">In future tutorials, we dive deeper into topics such as controllers, controller actions, views, view data, and HTML helpers.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="2af27-352">下一页</span><span class="sxs-lookup"><span data-stu-id="2af27-352">Next</span></span>](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb.md)
