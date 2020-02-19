---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
title: 添加模型 |Microsoft Docs
author: Rick-Anderson
description: 注意：本教程的更新版本可在此处使用 ASP.NET MVC 5 和 Visual Studio 2013。 更安全、更简单的操作和演示 。
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 53db72da-e0b9-44d9-b60b-6e6988c00b28
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: a9851d93dde495814f67fa0c807d3534f5f0d8ef
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457799"
---
# <a name="adding-a-model"></a><span data-ttu-id="2a23c-104">添加模型</span><span class="sxs-lookup"><span data-stu-id="2a23c-104">Adding a Model</span></span>

<span data-ttu-id="2a23c-105">作者： [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="2a23c-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="2a23c-106">[此处](../../getting-started/introduction/getting-started.md)提供了本教程的更新版本，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="2a23c-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="2a23c-107">更安全的方法是遵循更多功能，并演示更多的功能。</span><span class="sxs-lookup"><span data-stu-id="2a23c-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>

<span data-ttu-id="2a23c-108">在本部分中，你将添加一些用于在数据库中管理电影的类。</span><span class="sxs-lookup"><span data-stu-id="2a23c-108">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="2a23c-109">这些类将作为 ASP.NET MVC 应用程序&quot; 一部分的 &quot;模型。</span><span class="sxs-lookup"><span data-stu-id="2a23c-109">These classes will be the &quot;model&quot; part of the ASP.NET MVC application.</span></span>

<span data-ttu-id="2a23c-110">您将使用一种称为[实体框架](https://msdn.microsoft.com/library/bb399572(VS.110).aspx)的 .NET Framework 数据访问技术来定义和使用这些模型类。</span><span class="sxs-lookup"><span data-stu-id="2a23c-110">You'll use a .NET Framework data-access technology known as the [Entity Framework](https://msdn.microsoft.com/library/bb399572(VS.110).aspx) to define and work with these model classes.</span></span> <span data-ttu-id="2a23c-111">实体框架（通常称为 EF）支持名为*Code First*的开发模式。</span><span class="sxs-lookup"><span data-stu-id="2a23c-111">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="2a23c-112">Code First 允许通过编写简单的类来创建模型对象。</span><span class="sxs-lookup"><span data-stu-id="2a23c-112">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="2a23c-113">（这些类也称为 POCO 类，来自 &quot;纯传统 CLR 对象。&quot;）然后，你可以从类动态创建数据库，这样就可以实现非常干净且快速的开发工作流。</span><span class="sxs-lookup"><span data-stu-id="2a23c-113">(These are also known as POCO classes, from &quot;plain-old CLR objects.&quot;) You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="2a23c-114">添加模型类</span><span class="sxs-lookup"><span data-stu-id="2a23c-114">Adding Model Classes</span></span>

<span data-ttu-id="2a23c-115">在**解决方案资源管理器**中，右键单击 "*模型*" 文件夹，选择 "**添加**"，然后选择 "**类**"。</span><span class="sxs-lookup"><span data-stu-id="2a23c-115">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="2a23c-116">输入 &quot;Movie&quot;的*类*名。</span><span class="sxs-lookup"><span data-stu-id="2a23c-116">Enter the *class* name &quot;Movie&quot;.</span></span>

<span data-ttu-id="2a23c-117">将以下五个属性添加到 `Movie` 类：</span><span class="sxs-lookup"><span data-stu-id="2a23c-117">Add the following five properties to the `Movie` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

<span data-ttu-id="2a23c-118">我们将使用 `Movie` 类来表示数据库中的影片。</span><span class="sxs-lookup"><span data-stu-id="2a23c-118">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="2a23c-119">`Movie` 对象的每个实例都对应于数据库表中的一行，而 `Movie` 类的每个属性都将映射到该表中的列。</span><span class="sxs-lookup"><span data-stu-id="2a23c-119">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="2a23c-120">在同一文件中，添加以下 `MovieDBContext` 类：</span><span class="sxs-lookup"><span data-stu-id="2a23c-120">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample2.cs)]

<span data-ttu-id="2a23c-121">`MovieDBContext` 类表示实体框架的电影数据库上下文，用于处理数据库中 `Movie` 类实例的提取、存储和更新。</span><span class="sxs-lookup"><span data-stu-id="2a23c-121">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="2a23c-122">`MovieDBContext` 从实体框架提供的 `DbContext` 基类派生。</span><span class="sxs-lookup"><span data-stu-id="2a23c-122">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span>

<span data-ttu-id="2a23c-123">为了能够引用 `DbContext` 和 `DbSet`，需要在文件的顶部添加以下 `using` 语句：</span><span class="sxs-lookup"><span data-stu-id="2a23c-123">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `using` statement at the top of the file:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

<span data-ttu-id="2a23c-124">完整的*Movie.cs*文件如下所示。</span><span class="sxs-lookup"><span data-stu-id="2a23c-124">The complete *Movie.cs* file is shown below.</span></span> <span data-ttu-id="2a23c-125">（已删除多个不需要的 using 语句。）</span><span class="sxs-lookup"><span data-stu-id="2a23c-125">(Several using statements that are not needed have been removed.)</span></span>

[!code-csharp[Main](adding-a-model/samples/sample4.cs)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a><span data-ttu-id="2a23c-126">创建连接字符串并使用 SQL Server LocalDB</span><span class="sxs-lookup"><span data-stu-id="2a23c-126">Creating a Connection String and Working with SQL Server LocalDB</span></span>

<span data-ttu-id="2a23c-127">你创建的 `MovieDBContext` 类将处理连接到数据库的任务，并将 `Movie` 对象映射到数据库记录。</span><span class="sxs-lookup"><span data-stu-id="2a23c-127">The `MovieDBContext` class you created handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="2a23c-128">但您可能会问的一个问题是如何指定它将连接到的数据库。</span><span class="sxs-lookup"><span data-stu-id="2a23c-128">One question you might ask, though, is how to specify which database it will connect to.</span></span> <span data-ttu-id="2a23c-129">可以通过在应用程序的*web.config 文件中*添加连接信息来实现此目的。</span><span class="sxs-lookup"><span data-stu-id="2a23c-129">You'll do that by adding connection information in the *Web.config* file of the application.</span></span>

<span data-ttu-id="2a23c-130">打开应用程序根*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="2a23c-130">Open the application root *Web.config* file.</span></span> <span data-ttu-id="2a23c-131">（而不是*Views*文件夹中的*web.config 文件。* ）打开以红色列出的*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="2a23c-131">(Not the *Web.config* file in the *Views* folder.) Open the *Web.config* file outlined in red.</span></span>

![](adding-a-model/_static/image2.png)

<span data-ttu-id="2a23c-132">将以下连接字符串添加到*web.config 文件中的 `<connectionStrings>`* 元素。</span><span class="sxs-lookup"><span data-stu-id="2a23c-132">Add the following connection string to the `<connectionStrings>` element in the *Web.config* file.</span></span>

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

<span data-ttu-id="2a23c-133">下面的示例演示了*web.config 文件的*一部分，并添加了新的连接字符串：</span><span class="sxs-lookup"><span data-stu-id="2a23c-133">The following example shows a portion of the *Web.config* file with the new connection string added:</span></span>

[!code-xml[Main](adding-a-model/samples/sample6.xml?highlight=6-9)]

<span data-ttu-id="2a23c-134">这少量的代码和 XML 是您需要编写的所有内容，以表示和将电影数据存储在数据库中。</span><span class="sxs-lookup"><span data-stu-id="2a23c-134">This small amount of code and XML is everything you need to write in order to represent and store the movie data in a database.</span></span>

<span data-ttu-id="2a23c-135">接下来，您将生成一个新的 `MoviesController` 类，该类可用于显示电影数据并允许用户创建新的电影节目表。</span><span class="sxs-lookup"><span data-stu-id="2a23c-135">Next, you'll build a new `MoviesController` class that you can use to display the movie data and allow users to create new movie listings.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2a23c-136">[上一页](adding-a-view.md)
> [下一页](accessing-your-models-data-from-a-controller.md)</span><span class="sxs-lookup"><span data-stu-id="2a23c-136">[Previous](adding-a-view.md)
[Next](accessing-your-models-data-from-a-controller.md)</span></span>
