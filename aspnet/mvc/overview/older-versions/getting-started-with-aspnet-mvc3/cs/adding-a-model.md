---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-model
title: 添加模型（C#） |Microsoft Docs
author: Rick-Anderson
description: 注意：本教程的更新版本可在此处使用 ASP.NET MVC 5 和 Visual Studio 2013。 更安全、更简单的操作和演示 。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 42355b95-5f1f-413e-8d16-14cdfaaefcd8
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: a5f494eaa05bcfcd9d49873db728d71c1fd332c8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78434894"
---
# <a name="adding-a-model-c"></a><span data-ttu-id="62ade-104">添加模型 (C#)</span><span class="sxs-lookup"><span data-stu-id="62ade-104">Adding a Model (C#)</span></span>

<span data-ttu-id="62ade-105">作者： [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="62ade-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="62ade-106">本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 （Microsoft Visual Studio 免费版）生成 ASP.NET MVC Web 应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="62ade-106">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="62ade-107">在开始之前，请确保已安装下列必备组件。</span><span class="sxs-lookup"><span data-stu-id="62ade-107">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="62ade-108">可以通过单击以下链接安装所有这些[程序： Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="62ade-108">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="62ade-109">或者，你可以使用以下链接单独安装必备组件：</span><span class="sxs-lookup"><span data-stu-id="62ade-109">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="62ade-110">Visual Studio Web Developer Express SP1 必备组件</span><span class="sxs-lookup"><span data-stu-id="62ade-110">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="62ade-111">ASP.NET MVC 3 工具更新</span><span class="sxs-lookup"><span data-stu-id="62ade-111">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="62ade-112">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时 + 工具支持）</span><span class="sxs-lookup"><span data-stu-id="62ade-112">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="62ade-113">如果你使用的是 Visual Studio 2010 而不是 Visual Web Developer 2010，请通过单击以下链接安装必备组件： [Visual Studio 2010 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="62ade-113">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="62ade-114">本主题提供了包含C#源代码的 Visual Web Developer 项目。</span><span class="sxs-lookup"><span data-stu-id="62ade-114">A Visual Web Developer project with C# source code is available to accompany this topic.</span></span> <span data-ttu-id="62ade-115">[下载C#版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。</span><span class="sxs-lookup"><span data-stu-id="62ade-115">[Download the C# version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="62ade-116">如果希望 Visual Basic，请切换到本教程的[Visual Basic 版本](../vb/adding-a-model.md)。</span><span class="sxs-lookup"><span data-stu-id="62ade-116">If you prefer Visual Basic, switch to the [Visual Basic version](../vb/adding-a-model.md) of this tutorial.</span></span>

## <a name="adding-a-model"></a><span data-ttu-id="62ade-117">添加模型</span><span class="sxs-lookup"><span data-stu-id="62ade-117">Adding a Model</span></span>

<span data-ttu-id="62ade-118">在本部分中，你将添加一些用于在数据库中管理电影的类。</span><span class="sxs-lookup"><span data-stu-id="62ade-118">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="62ade-119">这些类将是 ASP.NET MVC 应用程序的 "模型" 部分。</span><span class="sxs-lookup"><span data-stu-id="62ade-119">These classes will be the "model" part of the ASP.NET MVC application.</span></span>

<span data-ttu-id="62ade-120">您将使用一种称为实体框架的 .NET Framework 数据访问技术来定义和使用这些模型类。</span><span class="sxs-lookup"><span data-stu-id="62ade-120">You'll use a .NET Framework data-access technology known as the Entity Framework to define and work with these model classes.</span></span> <span data-ttu-id="62ade-121">实体框架（通常称为 EF）支持名为*Code First*的开发模式。</span><span class="sxs-lookup"><span data-stu-id="62ade-121">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="62ade-122">Code First 允许通过编写简单的类来创建模型对象。</span><span class="sxs-lookup"><span data-stu-id="62ade-122">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="62ade-123">（这些类也称为 POCO 类，来自 "纯旧 CLR 对象"）。然后，你可以从类动态创建数据库，这样就可以实现非常干净且快速的开发工作流。</span><span class="sxs-lookup"><span data-stu-id="62ade-123">(These are also known as POCO classes, from "plain-old CLR objects.") You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="62ade-124">添加模型类</span><span class="sxs-lookup"><span data-stu-id="62ade-124">Adding Model Classes</span></span>

<span data-ttu-id="62ade-125">在**解决方案资源管理器**中，右键单击 "*模型*" 文件夹，选择 "**添加**"，然后选择 "**类**"。</span><span class="sxs-lookup"><span data-stu-id="62ade-125">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="62ade-126">将*类*命名为 "Movie"。</span><span class="sxs-lookup"><span data-stu-id="62ade-126">Name the *class* "Movie".</span></span>

<span data-ttu-id="62ade-127">[![CreateMovieClass](adding-a-model/_static/image3.png)](adding-a-model/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="62ade-127">[![CreateMovieClass](adding-a-model/_static/image3.png)](adding-a-model/_static/image2.png)</span></span>

<span data-ttu-id="62ade-128">将以下五个属性添加到 `Movie` 类：</span><span class="sxs-lookup"><span data-stu-id="62ade-128">Add the following five properties to the `Movie` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

<span data-ttu-id="62ade-129">我们将使用 `Movie` 类来表示数据库中的影片。</span><span class="sxs-lookup"><span data-stu-id="62ade-129">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="62ade-130">`Movie` 对象的每个实例都对应于数据库表中的一行，而 `Movie` 类的每个属性都将映射到该表中的列。</span><span class="sxs-lookup"><span data-stu-id="62ade-130">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="62ade-131">在同一文件中，添加以下 `MovieDBContext` 类：</span><span class="sxs-lookup"><span data-stu-id="62ade-131">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample2.cs)]

<span data-ttu-id="62ade-132">`MovieDBContext` 类表示实体框架的电影数据库上下文，用于处理数据库中 `Movie` 类实例的提取、存储和更新。</span><span class="sxs-lookup"><span data-stu-id="62ade-132">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="62ade-133">`MovieDBContext` 从实体框架提供的 `DbContext` 基类派生。</span><span class="sxs-lookup"><span data-stu-id="62ade-133">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span> <span data-ttu-id="62ade-134">有关 `DbContext` 和 `DbSet`的详细信息，请参阅[实体框架的工作效率改进](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0)。</span><span class="sxs-lookup"><span data-stu-id="62ade-134">For more information about `DbContext` and `DbSet`, see [Productivity Improvements for the Entity Framework](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0).</span></span>

<span data-ttu-id="62ade-135">为了能够引用 `DbContext` 和 `DbSet`，需要在文件的顶部添加以下 `using` 语句：</span><span class="sxs-lookup"><span data-stu-id="62ade-135">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `using` statement at the top of the file:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

<span data-ttu-id="62ade-136">完整的*Movie.cs*文件如下所示。</span><span class="sxs-lookup"><span data-stu-id="62ade-136">The complete *Movie.cs* file is shown below.</span></span>

[!code-csharp[Main](adding-a-model/samples/sample4.cs)]

## <a name="creating-a-connection-string-and-working-with-sql-server-compact"></a><span data-ttu-id="62ade-137">创建连接字符串并使用 SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="62ade-137">Creating a Connection String and Working with SQL Server Compact</span></span>

<span data-ttu-id="62ade-138">你创建的 `MovieDBContext` 类将处理连接到数据库的任务，并将 `Movie` 对象映射到数据库记录。</span><span class="sxs-lookup"><span data-stu-id="62ade-138">The `MovieDBContext` class you created handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="62ade-139">但您可能会问的一个问题是如何指定它将连接到的数据库。</span><span class="sxs-lookup"><span data-stu-id="62ade-139">One question you might ask, though, is how to specify which database it will connect to.</span></span> <span data-ttu-id="62ade-140">可以通过在应用程序的*web.config 文件中*添加连接信息来实现此目的。</span><span class="sxs-lookup"><span data-stu-id="62ade-140">You'll do that by adding connection information in the *Web.config* file of the application.</span></span>

<span data-ttu-id="62ade-141">打开应用程序根*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="62ade-141">Open the application root *Web.config* file.</span></span> <span data-ttu-id="62ade-142">（而不是*Views*文件夹中的*web.config 文件。* ）下图显示了*web.config*文件;打开以红色*圆圈表示的 web.config 文件*。</span><span class="sxs-lookup"><span data-stu-id="62ade-142">(Not the *Web.config* file in the *Views* folder.) The image below show both *Web.config* files; open the *Web.config* file circled in red.</span></span>

![](adding-a-model/_static/image4.png)

<span data-ttu-id="62ade-143">将以下连接字符串添加到*web.config 文件中的 `<connectionStrings>`* 元素。</span><span class="sxs-lookup"><span data-stu-id="62ade-143">Add the following connection string to the `<connectionStrings>` element in the *Web.config* file.</span></span>

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

<span data-ttu-id="62ade-144">下面的示例演示了*web.config 文件的*一部分，并添加了新的连接字符串：</span><span class="sxs-lookup"><span data-stu-id="62ade-144">The following example shows a portion of the *Web.config* file with the new connection string added:</span></span>

[!code-xml[Main](adding-a-model/samples/sample6.xml)]

<span data-ttu-id="62ade-145">这少量的代码和 XML 是您需要编写的所有内容，以表示和将电影数据存储在数据库中。</span><span class="sxs-lookup"><span data-stu-id="62ade-145">This small amount of code and XML is everything you need to write in order to represent and store the movie data in a database.</span></span>

<span data-ttu-id="62ade-146">接下来，您将生成一个新的 `MoviesController` 类，该类可用于显示电影数据并允许用户创建新的电影节目表。</span><span class="sxs-lookup"><span data-stu-id="62ade-146">Next, you'll build a new `MoviesController` class that you can use to display the movie data and allow users to create new movie listings.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="62ade-147">[上一页](adding-a-view.md)
> [下一页](accessing-your-models-data-from-a-controller.md)</span><span class="sxs-lookup"><span data-stu-id="62ade-147">[Previous](adding-a-view.md)
[Next](accessing-your-models-data-from-a-controller.md)</span></span>
