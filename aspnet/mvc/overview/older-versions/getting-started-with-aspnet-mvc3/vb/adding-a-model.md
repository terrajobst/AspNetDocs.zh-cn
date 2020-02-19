---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-model
title: 添加模型（VB） |Microsoft Docs
author: Rick-Anderson
description: 本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 构建 ASP.NET MVC Web 应用程序的基础知识 。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: b3aa7720-5c78-4ca2-baef-9a52234fb7ce
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: e69d59aed4d74f08f1c653c4965b128c4dbe20ff
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457240"
---
# <a name="adding-a-model-vb"></a><span data-ttu-id="5a613-103">添加模型 (VB)</span><span class="sxs-lookup"><span data-stu-id="5a613-103">Adding a Model (VB)</span></span>

<span data-ttu-id="5a613-104">作者： [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="5a613-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="5a613-105">本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 （Microsoft Visual Studio 免费版）生成 ASP.NET MVC Web 应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="5a613-105">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="5a613-106">在开始之前，请确保已安装下列必备组件。</span><span class="sxs-lookup"><span data-stu-id="5a613-106">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="5a613-107">可以通过单击以下链接安装所有这些[程序： Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="5a613-107">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="5a613-108">或者，你可以使用以下链接单独安装必备组件：</span><span class="sxs-lookup"><span data-stu-id="5a613-108">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="5a613-109">Visual Studio Web Developer Express SP1 必备组件</span><span class="sxs-lookup"><span data-stu-id="5a613-109">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="5a613-110">ASP.NET MVC 3 工具更新</span><span class="sxs-lookup"><span data-stu-id="5a613-110">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="5a613-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时 + 工具支持）</span><span class="sxs-lookup"><span data-stu-id="5a613-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="5a613-112">如果你使用的是 Visual Studio 2010 而不是 Visual Web Developer 2010，请通过单击以下链接安装必备组件： [Visual Studio 2010 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="5a613-112">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="5a613-113">本主题附带有 VB.NET 源代码的 Visual Web Developer 项目。</span><span class="sxs-lookup"><span data-stu-id="5a613-113">A Visual Web Developer project with VB.NET source code is available to accompany this topic.</span></span> <span data-ttu-id="5a613-114">[下载 VB.NET 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。</span><span class="sxs-lookup"><span data-stu-id="5a613-114">[Download the VB.NET version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="5a613-115">如果愿意C#，请切换到本教程的[ C#版本](../cs/adding-a-model.md)。</span><span class="sxs-lookup"><span data-stu-id="5a613-115">If you prefer C#, switch to the [C# version](../cs/adding-a-model.md) of this tutorial.</span></span>

## <a name="adding-a-model"></a><span data-ttu-id="5a613-116">添加模型</span><span class="sxs-lookup"><span data-stu-id="5a613-116">Adding a Model</span></span>

<span data-ttu-id="5a613-117">在本部分中，你将添加一些用于在数据库中管理电影的类。</span><span class="sxs-lookup"><span data-stu-id="5a613-117">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="5a613-118">这些类将是 ASP.NET MVC 应用程序的 "模型" 部分。</span><span class="sxs-lookup"><span data-stu-id="5a613-118">These classes will be the "model" part of the ASP.NET MVC application.</span></span>

<span data-ttu-id="5a613-119">您将使用一种称为实体框架的 .NET Framework 数据访问技术来定义和使用这些模型类。</span><span class="sxs-lookup"><span data-stu-id="5a613-119">You'll use a .NET Framework data-access technology known as the Entity Framework to define and work with these model classes.</span></span> <span data-ttu-id="5a613-120">实体框架（通常称为 EF）支持名为*Code First*的开发模式。</span><span class="sxs-lookup"><span data-stu-id="5a613-120">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="5a613-121">Code First 允许通过编写简单的类来创建模型对象。</span><span class="sxs-lookup"><span data-stu-id="5a613-121">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="5a613-122">（这些类也称为 POCO 类，来自 "纯旧 CLR 对象"）。然后，你可以从类动态创建数据库，这样就可以实现非常干净且快速的开发工作流。</span><span class="sxs-lookup"><span data-stu-id="5a613-122">(These are also known as POCO classes, from "plain-old CLR objects.") You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="5a613-123">添加模型类</span><span class="sxs-lookup"><span data-stu-id="5a613-123">Adding Model Classes</span></span>

<span data-ttu-id="5a613-124">在**解决方案资源管理器**中，右键单击 "*模型*" 文件夹，选择 "**添加**"，然后选择 "**类**"。</span><span class="sxs-lookup"><span data-stu-id="5a613-124">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="5a613-125">将类命名为 "Movie"。</span><span class="sxs-lookup"><span data-stu-id="5a613-125">Name the class "Movie".</span></span>

<span data-ttu-id="5a613-126">将以下五个属性添加到 `Movie` 类：</span><span class="sxs-lookup"><span data-stu-id="5a613-126">Add the following five properties to the `Movie` class:</span></span>

[!code-vb[Main](adding-a-model/samples/sample1.vb)]

<span data-ttu-id="5a613-127">我们将使用 `Movie` 类来表示数据库中的影片。</span><span class="sxs-lookup"><span data-stu-id="5a613-127">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="5a613-128">`Movie` 对象的每个实例都对应于数据库表中的一行，而 `Movie` 类的每个属性都将映射到该表中的列。</span><span class="sxs-lookup"><span data-stu-id="5a613-128">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="5a613-129">在同一文件中，添加以下 `MovieDBContext` 类：</span><span class="sxs-lookup"><span data-stu-id="5a613-129">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-vb[Main](adding-a-model/samples/sample2.vb)]

<span data-ttu-id="5a613-130">`MovieDBContext` 类表示实体框架的电影数据库上下文，用于处理数据库中 `Movie` 类实例的提取、存储和更新。</span><span class="sxs-lookup"><span data-stu-id="5a613-130">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="5a613-131">`MovieDBContext` 从实体框架提供的 `DbContext` 基类派生。</span><span class="sxs-lookup"><span data-stu-id="5a613-131">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span> <span data-ttu-id="5a613-132">有关 `DbContext` 和 `DbSet`的详细信息，请参阅[实体框架的工作效率改进](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0)。</span><span class="sxs-lookup"><span data-stu-id="5a613-132">For more information about `DbContext` and `DbSet`, see [Productivity Improvements for the Entity Framework](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0).</span></span>

<span data-ttu-id="5a613-133">为了能够引用 `DbContext` 和 `DbSet`，需要在文件的顶部添加以下 `imports` 语句：</span><span class="sxs-lookup"><span data-stu-id="5a613-133">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `imports` statement at the top of the file:</span></span>

[!code-vb[Main](adding-a-model/samples/sample3.vb)]

<span data-ttu-id="5a613-134">下面显示了完整的*Movie .vb*文件。</span><span class="sxs-lookup"><span data-stu-id="5a613-134">The complete *Movie.vb* file is shown below.</span></span>

[!code-vb[Main](adding-a-model/samples/sample4.vb)]

## <a name="creating-a-connection-string-and-working-with-sql-server-compact"></a><span data-ttu-id="5a613-135">创建连接字符串并使用 SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="5a613-135">Creating a Connection String and Working with SQL Server Compact</span></span>

<span data-ttu-id="5a613-136">你创建的 `MovieDBContext` 类将处理连接到数据库的任务，并将 `Movie` 对象映射到数据库记录。</span><span class="sxs-lookup"><span data-stu-id="5a613-136">The `MovieDBContext` class you created handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="5a613-137">但您可能会问的一个问题是如何指定它将连接到的数据库。</span><span class="sxs-lookup"><span data-stu-id="5a613-137">One question you might ask, though, is how to specify which database it will connect to.</span></span> <span data-ttu-id="5a613-138">可以通过在应用程序的*web.config 文件中*添加连接信息来实现此目的。</span><span class="sxs-lookup"><span data-stu-id="5a613-138">You'll do that by adding connection information in the *Web.config* file of the application.</span></span>

<span data-ttu-id="5a613-139">打开应用程序根*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="5a613-139">Open the application root *Web.config* file.</span></span> <span data-ttu-id="5a613-140">（而不是*Views*文件夹中的*web.config 文件。* ）下图显示了*web.config*文件;打开以红色*圆圈表示的 web.config 文件*。</span><span class="sxs-lookup"><span data-stu-id="5a613-140">(Not the *Web.config* file in the *Views* folder.) The image below show both *Web.config* files; open the *Web.config* file circled in red.</span></span>

![](adding-a-model/_static/image2.png)

<span data-ttu-id="5a613-141">将以下连接字符串添加到*web.config 文件中的 `<connectionStrings>`* 元素。</span><span class="sxs-lookup"><span data-stu-id="5a613-141">Add the following connection string to the `<connectionStrings>` element in the *Web.config* file.</span></span>

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

<span data-ttu-id="5a613-142">下面的示例演示了*web.config 文件的*一部分，并添加了新的连接字符串：</span><span class="sxs-lookup"><span data-stu-id="5a613-142">The following example shows a portion of the *Web.config* file with the new connection string added:</span></span>

[!code-xml[Main](adding-a-model/samples/sample6.xml)]

<span data-ttu-id="5a613-143">这少量的代码和 XML 是您需要编写的所有内容，以表示和将电影数据存储在数据库中。</span><span class="sxs-lookup"><span data-stu-id="5a613-143">This small amount of code and XML is everything you need to write in order to represent and store the movie data in a database.</span></span>

<span data-ttu-id="5a613-144">接下来，您将生成一个新的 `MoviesController` 类，该类可用于显示电影数据并允许用户创建新的电影节目表。</span><span class="sxs-lookup"><span data-stu-id="5a613-144">Next, you'll build a new `MoviesController` class that you can use to display the movie data and allow users to create new movie listings.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5a613-145">[上一页](adding-a-view.md)
> [下一页](accessing-your-models-data-from-a-controller.md)</span><span class="sxs-lookup"><span data-stu-id="5a613-145">[Previous](adding-a-view.md)
[Next](accessing-your-models-data-from-a-controller.md)</span></span>
