---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create_the_data_access_layer
title: 创建数据访问层 |Microsoft Docs
author: Erikre
description: 本系列教程将介绍使用 ASP.NET 4.5 构建 ASP.NET Web 窗体应用程序的基础知识，并为我们 Microsoft Visual Studio Express 2013 。
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 0bbf7a6e-d7eb-4091-91e4-fff892777f32
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create_the_data_access_layer
msc.type: authoredcontent
ms.openlocfilehash: 0fcf050474a57be9ed53ec0783a6d6b7dde2bf4c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78438374"
---
# <a name="create-the-data-access-layer"></a><span data-ttu-id="62458-103">创建数据访问层</span><span class="sxs-lookup"><span data-stu-id="62458-103">Create the Data Access Layer</span></span>

<span data-ttu-id="62458-104">作者： [Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="62458-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="62458-105">[下载 Wingtip 玩具示例项目（C#）](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下载电子书（PDF）](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="62458-105">[Download Wingtip Toys Sample Project (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

> <span data-ttu-id="62458-106">本系列教程将介绍使用 ASP.NET 4.5 构建 ASP.NET Web 窗体应用程序的基础知识，并为 Web Microsoft Visual Studio Express 2013。</span><span class="sxs-lookup"><span data-stu-id="62458-106">This tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="62458-107">此教程系列附带有[ C#源代码](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)的 Visual Studio 2013 项目。</span><span class="sxs-lookup"><span data-stu-id="62458-107">A Visual Studio 2013 [project with C# source code](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) is available to accompany this tutorial series.</span></span>

<span data-ttu-id="62458-108">本教程介绍如何使用 ASP.NET Web 窗体和实体框架 Code First 从数据库创建、访问和查看数据。</span><span class="sxs-lookup"><span data-stu-id="62458-108">This tutorial describes how to create, access, and review data from a database using ASP.NET Web Forms and Entity Framework Code First.</span></span> <span data-ttu-id="62458-109">本教程基于前面的 "创建项目" 教程，是 Wingtip 玩具应用商店教程系列的一部分。</span><span class="sxs-lookup"><span data-stu-id="62458-109">This tutorial builds on the previous tutorial "Create the Project" and is part of the Wingtip Toy Store tutorial series.</span></span> <span data-ttu-id="62458-110">完成本教程后，您将生成一组数据访问类，这些类位于项目的 "*模型*" 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="62458-110">When you've completed this tutorial, you will have built a group of data-access classes that are in the *Models* folder of the project.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="62458-111">学习内容：</span><span class="sxs-lookup"><span data-stu-id="62458-111">What you'll learn:</span></span>

- <span data-ttu-id="62458-112">如何创建数据模型。</span><span class="sxs-lookup"><span data-stu-id="62458-112">How to create the data models.</span></span>
- <span data-ttu-id="62458-113">如何初始化和播种数据库。</span><span class="sxs-lookup"><span data-stu-id="62458-113">How to initialize and seed the database.</span></span>
- <span data-ttu-id="62458-114">如何更新和配置应用程序以支持数据库。</span><span class="sxs-lookup"><span data-stu-id="62458-114">How to update and configure the application to support the database.</span></span>

### <a name="these-are-the-features-introduced-in-the-tutorial"></a><span data-ttu-id="62458-115">这些是教程中引入的功能：</span><span class="sxs-lookup"><span data-stu-id="62458-115">These are the features introduced in the tutorial:</span></span>

- <span data-ttu-id="62458-116">实体框架 Code First</span><span class="sxs-lookup"><span data-stu-id="62458-116">Entity Framework Code First</span></span>
- <span data-ttu-id="62458-117">LocalDB</span><span class="sxs-lookup"><span data-stu-id="62458-117">LocalDB</span></span>
- <span data-ttu-id="62458-118">数据注释</span><span class="sxs-lookup"><span data-stu-id="62458-118">Data Annotations</span></span>

## <a name="creating-the-data-models"></a><span data-ttu-id="62458-119">创建数据模型</span><span class="sxs-lookup"><span data-stu-id="62458-119">Creating the Data Models</span></span>

<span data-ttu-id="62458-120">[实体框架](https://msdn.microsoft.com/data/aa937723)是对象关系映射（ORM）框架。</span><span class="sxs-lookup"><span data-stu-id="62458-120">[Entity Framework](https://msdn.microsoft.com/data/aa937723) is an object-relational mapping (ORM) framework.</span></span> <span data-ttu-id="62458-121">它使您可以将关系数据作为对象处理，从而消除了通常需要编写的大部分数据访问代码。</span><span class="sxs-lookup"><span data-stu-id="62458-121">It lets you work with relational data as objects, eliminating most of the data-access code that you'd usually need to write.</span></span> <span data-ttu-id="62458-122">使用实体框架，可以使用[LINQ](https://msdn.microsoft.com/library/bb397926.aspx)发出查询，然后将数据作为强类型对象检索和操作。</span><span class="sxs-lookup"><span data-stu-id="62458-122">Using Entity Framework, you can issue queries using [LINQ](https://msdn.microsoft.com/library/bb397926.aspx), then retrieve and manipulate data as strongly typed objects.</span></span> <span data-ttu-id="62458-123">LINQ 提供了用于查询和更新数据的模式。</span><span class="sxs-lookup"><span data-stu-id="62458-123">LINQ provides patterns for querying and updating data.</span></span> <span data-ttu-id="62458-124">使用实体框架使你可以专注于创建应用程序的其余部分，而不是专注于数据访问基础知识。</span><span class="sxs-lookup"><span data-stu-id="62458-124">Using Entity Framework allows you to focus on creating the rest of your application, rather than focusing on the data access fundamentals.</span></span> <span data-ttu-id="62458-125">稍后在本系列教程中，我们将向您演示如何使用数据来填充导航和产品查询。</span><span class="sxs-lookup"><span data-stu-id="62458-125">Later in this tutorial series, we'll show you how to use the data to populate navigation and product queries.</span></span>

<span data-ttu-id="62458-126">实体框架支持名为*Code First*的开发模式。</span><span class="sxs-lookup"><span data-stu-id="62458-126">Entity Framework supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="62458-127">Code First 允许使用类定义数据模型。</span><span class="sxs-lookup"><span data-stu-id="62458-127">Code First lets you define your data models using classes.</span></span> <span data-ttu-id="62458-128">类是一种构造，使你能够通过将其他类型、方法和事件的变量组合在一起来创建自己的自定义类型。</span><span class="sxs-lookup"><span data-stu-id="62458-128">A class is a construct that enables you to create your own custom types by grouping together variables of other types, methods and events.</span></span> <span data-ttu-id="62458-129">您可以将类映射到现有数据库，或使用它们来生成数据库。</span><span class="sxs-lookup"><span data-stu-id="62458-129">You can map classes to an existing database or use them to generate a database.</span></span> <span data-ttu-id="62458-130">在本教程中，您将通过编写数据模型类来创建数据模型。</span><span class="sxs-lookup"><span data-stu-id="62458-130">In this tutorial, you'll create the data models by writing data model classes.</span></span> <span data-ttu-id="62458-131">接下来，您将实体框架从这些新类动态创建数据库。</span><span class="sxs-lookup"><span data-stu-id="62458-131">Then, you'll let Entity Framework create the database on the fly from these new classes.</span></span>

<span data-ttu-id="62458-132">首先，您将创建为 Web 窗体应用程序定义数据模型的实体类。</span><span class="sxs-lookup"><span data-stu-id="62458-132">You will begin by creating the entity classes that define the data models for the Web Forms application.</span></span> <span data-ttu-id="62458-133">然后，将创建一个上下文类，该类用于管理实体类并提供对数据库的数据访问。</span><span class="sxs-lookup"><span data-stu-id="62458-133">Then you will create a context class that manages the entity classes and provides data access to the database.</span></span> <span data-ttu-id="62458-134">你还将创建一个用于填充数据库的初始化表达式类。</span><span class="sxs-lookup"><span data-stu-id="62458-134">You will also create an initializer class that you will use to populate the database.</span></span>

### <a name="entity-framework-and-references"></a><span data-ttu-id="62458-135">实体框架和引用</span><span class="sxs-lookup"><span data-stu-id="62458-135">Entity Framework and References</span></span>

<span data-ttu-id="62458-136">默认情况下，当你使用**Web 窗体**模板创建新的**ASP.NET Web 应用程序**时，将包含实体框架。</span><span class="sxs-lookup"><span data-stu-id="62458-136">By default, Entity Framework is included when you create a new **ASP.NET Web Application** using the **Web Forms** template.</span></span> <span data-ttu-id="62458-137">可以安装、卸载实体框架，并将其更新为 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="62458-137">Entity Framework can be installed, uninstalled, and updated as a NuGet package.</span></span>

<span data-ttu-id="62458-138">此 NuGet 包包括项目中的以下**运行时**程序集：</span><span class="sxs-lookup"><span data-stu-id="62458-138">This NuGet package includes the following **runtime** assemblies within your project:</span></span>

- <span data-ttu-id="62458-139">EntityFramework-实体框架使用的所有常见运行时代码</span><span class="sxs-lookup"><span data-stu-id="62458-139">EntityFramework.dll – All the common runtime code used by Entity Framework</span></span>
- <span data-ttu-id="62458-140">EntityFramework –实体框架的 Microsoft SQL Server 提供程序</span><span class="sxs-lookup"><span data-stu-id="62458-140">EntityFramework.SqlServer.dll – The Microsoft SQL Server provider for Entity Framework</span></span>

### <a name="entity-classes"></a><span data-ttu-id="62458-141">实体类</span><span class="sxs-lookup"><span data-stu-id="62458-141">Entity Classes</span></span>

<span data-ttu-id="62458-142">你创建的用于定义数据架构的类称为实体类。</span><span class="sxs-lookup"><span data-stu-id="62458-142">The classes you create to define the schema of the data are called entity classes.</span></span> <span data-ttu-id="62458-143">如果您不熟悉数据库设计，请将实体类视为数据库的表定义。</span><span class="sxs-lookup"><span data-stu-id="62458-143">If you're new to database design, think of the entity classes as table definitions of a database.</span></span> <span data-ttu-id="62458-144">类中的每个属性指定数据库的表中的列。</span><span class="sxs-lookup"><span data-stu-id="62458-144">Each property in the class specifies a column in the table of the database.</span></span> <span data-ttu-id="62458-145">这些类提供了面向对象的代码与数据库的关系表结构之间的轻型对象关系接口。</span><span class="sxs-lookup"><span data-stu-id="62458-145">These classes provide a lightweight, object-relational interface between object-oriented code and the relational table structure of the database.</span></span>

<span data-ttu-id="62458-146">在本教程中，您将添加代表产品和类别的架构的简单实体类。</span><span class="sxs-lookup"><span data-stu-id="62458-146">In this tutorial, you'll start out by adding simple entity classes representing the schemas for products and categories.</span></span> <span data-ttu-id="62458-147">Products 类将包含每个产品的定义。</span><span class="sxs-lookup"><span data-stu-id="62458-147">The products class will contain definitions for each product.</span></span> <span data-ttu-id="62458-148">Product 类的每个成员的名称将为 `ProductID`、`ProductName`、`Description`、`ImagePath`、`UnitPrice`、`CategoryID`和 `Category`。</span><span class="sxs-lookup"><span data-stu-id="62458-148">The name of each of the members of the product class will be `ProductID`, `ProductName`, `Description`, `ImagePath`, `UnitPrice`, `CategoryID`, and `Category`.</span></span> <span data-ttu-id="62458-149">Category 类将包含产品可以属于的每个类别的定义，例如汽车、船或飞机。</span><span class="sxs-lookup"><span data-stu-id="62458-149">The category class will contain definitions for each category that a product can belong to, such as Car, Boat, or Plane.</span></span> <span data-ttu-id="62458-150">类别类的每个成员的名称将为 `CategoryID`、`CategoryName`、`Description`和 `Products`。</span><span class="sxs-lookup"><span data-stu-id="62458-150">The name of each of the members of the category class will be `CategoryID`, `CategoryName`, `Description`, and `Products`.</span></span> <span data-ttu-id="62458-151">每个产品都属于某个类别。</span><span class="sxs-lookup"><span data-stu-id="62458-151">Each product will belong to one of the categories.</span></span> <span data-ttu-id="62458-152">这些实体类将添加到项目的现有*模型*文件夹中。</span><span class="sxs-lookup"><span data-stu-id="62458-152">These entity classes will be added to the project's existing *Models* folder.</span></span>

1. <span data-ttu-id="62458-153">在**解决方案资源管理器**中，右键单击 "*模型*" 文件夹，然后选择 "**添加** -&gt;**新项**"。</span><span class="sxs-lookup"><span data-stu-id="62458-153">In **Solution Explorer**, right-click the *Models* folder and then select **Add** -&gt; **New Item**.</span></span> 

    ![创建数据访问层-新建项菜单](create_the_data_access_layer/_static/image1.png)

   <span data-ttu-id="62458-155">随即出现“添加新项”对话框。</span><span class="sxs-lookup"><span data-stu-id="62458-155">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="62458-156">在左侧的 "**已安装**" 窗格中，选择 "**代码**"。 **C#**</span><span class="sxs-lookup"><span data-stu-id="62458-156">Under **Visual C#** from the **Installed** pane on the left, select **Code**.</span></span> 

    ![创建数据访问层-新建项菜单](create_the_data_access_layer/_static/image2.png)
3. <span data-ttu-id="62458-158">从中间窗格中选择 "**类**"，并将此新类命名为*Product.cs*。</span><span class="sxs-lookup"><span data-stu-id="62458-158">Select **Class** from the middle pane and name this new class *Product.cs*.</span></span>
4. <span data-ttu-id="62458-159">单击 **“添加”** 。</span><span class="sxs-lookup"><span data-stu-id="62458-159">Click **Add**.</span></span>  
   <span data-ttu-id="62458-160">新的类文件将显示在编辑器中。</span><span class="sxs-lookup"><span data-stu-id="62458-160">The new class file is displayed in the editor.</span></span>
5. <span data-ttu-id="62458-161">将默认代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="62458-161">Replace the default code with the following code:</span></span>   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample1.cs)]
6. <span data-ttu-id="62458-162">通过重复步骤1到步骤4创建另一个类，但将新类命名为*Category.cs* ，并将默认代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="62458-162">Create another class by repeating steps 1 through 4, however, name the new class *Category.cs* and replace the default code with the following code:</span></span>  

    [!code-csharp[Main](create_the_data_access_layer/samples/sample2.cs)]

<span data-ttu-id="62458-163">如前所述，`Category` 类表示应用程序设计用于销售的产品类型（如<a id="a"></a>&quot;轿车&quot;、&quot;Boats&quot;、&quot;Rockets&quot;等），`Product` 类表示数据库中的各个产品（玩具）。</span><span class="sxs-lookup"><span data-stu-id="62458-163">As previously mentioned, the `Category` class represents the type of product that the application is designed to sell (such as <a id="a"></a>&quot;Cars&quot;, &quot;Boats&quot;, &quot;Rockets&quot;, and so on), and the `Product` class represents the individual products (toys) in the database.</span></span> <span data-ttu-id="62458-164">`Product` 对象的每个实例都对应于关系数据库表中的一行，Product 类的每个属性都将映射到关系数据库表中的一个列。</span><span class="sxs-lookup"><span data-stu-id="62458-164">Each instance of a `Product` object will correspond to a row within a relational database table, and each property of the Product class will map to a column in the relational database table.</span></span> <span data-ttu-id="62458-165">稍后在本教程中，你将查看数据库中包含的产品数据。</span><span class="sxs-lookup"><span data-stu-id="62458-165">Later in this tutorial, you'll review the product data contained in the database.</span></span>

### <a name="data-annotations"></a><span data-ttu-id="62458-166">数据注释</span><span class="sxs-lookup"><span data-stu-id="62458-166">Data Annotations</span></span>

<span data-ttu-id="62458-167">您可能已注意到，类的某些成员具有指定成员详细信息的属性，如 `[ScaffoldColumn(false)]`。</span><span class="sxs-lookup"><span data-stu-id="62458-167">You may have noticed that certain members of the classes have attributes specifying details about the member, such as `[ScaffoldColumn(false)]`.</span></span> <span data-ttu-id="62458-168">这些是*数据批注*。</span><span class="sxs-lookup"><span data-stu-id="62458-168">These are *data annotations*.</span></span> <span data-ttu-id="62458-169">数据批注属性可以描述如何验证该成员的用户输入、指定其格式设置，以及指定在创建数据库时如何对其进行建模。</span><span class="sxs-lookup"><span data-stu-id="62458-169">The data annotation attributes can describe how to validate user input for that member, to specify formatting for it, and to specify how it is modeled when the database is created.</span></span>

### <a name="context-class"></a><span data-ttu-id="62458-170">Context 类</span><span class="sxs-lookup"><span data-stu-id="62458-170">Context Class</span></span>

<span data-ttu-id="62458-171">若要开始使用类进行数据访问，必须定义一个上下文类。</span><span class="sxs-lookup"><span data-stu-id="62458-171">To start using the classes for data access, you must define a context class.</span></span> <span data-ttu-id="62458-172">如前所述，上下文类管理实体类（如 `Product` 类和 `Category` 类）并提供对数据库的数据访问。</span><span class="sxs-lookup"><span data-stu-id="62458-172">As mentioned previously, the context class manages the entity classes (such as the `Product` class and the `Category` class) and provides data access to the database.</span></span>

<span data-ttu-id="62458-173">此过程将新C#的上下文类添加到 "*模型*" 文件夹。</span><span class="sxs-lookup"><span data-stu-id="62458-173">This procedure adds a new C# context class to the *Models* folder.</span></span>

1. <span data-ttu-id="62458-174">右键单击 "*模型*" 文件夹，然后选择 "**添加** -&gt;**新项**"。</span><span class="sxs-lookup"><span data-stu-id="62458-174">Right-click the *Models* folder and then select **Add** -&gt; **New Item**.</span></span>   
   <span data-ttu-id="62458-175">随即出现“添加新项”对话框。</span><span class="sxs-lookup"><span data-stu-id="62458-175">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="62458-176">从中间窗格中选择 "**类**"，将其命名为*ProductContext.cs* ，然后单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="62458-176">Select **Class** from the middle pane, name it *ProductContext.cs* and click **Add**.</span></span>
3. <span data-ttu-id="62458-177">将类中包含的默认代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="62458-177">Replace the default code contained in the class with the following code:</span></span>   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample3.cs)]

<span data-ttu-id="62458-178">此代码将添加 `System.Data.Entity` 命名空间，以便您可以访问实体框架的所有核心功能，其中包括使用强类型对象查询、插入、更新和删除数据的功能。</span><span class="sxs-lookup"><span data-stu-id="62458-178">This code adds the `System.Data.Entity` namespace so that you have access to all the core functionality of Entity Framework, which includes the capability to query, insert, update, and delete data by working with strongly typed objects.</span></span>

<span data-ttu-id="62458-179">`ProductContext` 类表示实体框架产品数据库上下文，用于处理数据库中 `Product` 类实例的提取、存储和更新。</span><span class="sxs-lookup"><span data-stu-id="62458-179">The `ProductContext` class represents Entity Framework product database context, which handles fetching, storing, and updating `Product` class instances in the database.</span></span> <span data-ttu-id="62458-180">`ProductContext` 类从实体框架提供的 `DbContext` 基类派生。</span><span class="sxs-lookup"><span data-stu-id="62458-180">The `ProductContext` class derives from the `DbContext` base class provided by Entity Framework.</span></span>

### <a name="initializer-class"></a><span data-ttu-id="62458-181">初始值设定项类</span><span class="sxs-lookup"><span data-stu-id="62458-181">Initializer Class</span></span>

<span data-ttu-id="62458-182">第一次使用上下文时，需要运行一些自定义逻辑来初始化数据库。</span><span class="sxs-lookup"><span data-stu-id="62458-182">You will need to run some custom logic to initialize the database the first time the context is used.</span></span> <span data-ttu-id="62458-183">这将允许将种子数据添加到数据库，以便可以立即显示产品和类别。</span><span class="sxs-lookup"><span data-stu-id="62458-183">This will allow seed data to be added to the database so that you can immediately display products and categories.</span></span>

<span data-ttu-id="62458-184">此过程将新C#的初始值设定项类添加到*模型*文件夹中。</span><span class="sxs-lookup"><span data-stu-id="62458-184">This procedure adds a new C# initializer class to the *Models* folder.</span></span>

1. <span data-ttu-id="62458-185">在 "*模型*" 文件夹中创建另一个 `Class`，并将其命名为*ProductDatabaseInitializer.cs*。</span><span class="sxs-lookup"><span data-stu-id="62458-185">Create another `Class` in the *Models* folder and name it *ProductDatabaseInitializer.cs*.</span></span>
2. <span data-ttu-id="62458-186">将类中包含的默认代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="62458-186">Replace the default code contained in the class with the following code:</span></span>   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample4.cs)]

<span data-ttu-id="62458-187">如以上代码所示，在创建和初始化数据库时，将重写并设置 `Seed` 属性。</span><span class="sxs-lookup"><span data-stu-id="62458-187">As you can see from the above code, when the database is created and initialized, the `Seed` property is overridden and set.</span></span> <span data-ttu-id="62458-188">设置 `Seed` 属性后，将使用类别和产品中的值填充数据库。</span><span class="sxs-lookup"><span data-stu-id="62458-188">When the `Seed` property is set, the values from the categories and products are used to populate the database.</span></span> <span data-ttu-id="62458-189">如果尝试在创建数据库后通过修改上述代码来更新种子数据，则在运行 Web 应用程序时，将看不到任何更新。</span><span class="sxs-lookup"><span data-stu-id="62458-189">If you attempt to update the seed data by modifying the above code after the database has been created, you won't see any updates when you run the Web application.</span></span> <span data-ttu-id="62458-190">原因是上面的代码使用 `DropCreateDatabaseIfModelChanges` 类的实现来识别模型（架构）是否在重置种子数据之前已更改。</span><span class="sxs-lookup"><span data-stu-id="62458-190">The reason is the above code uses an implementation of the `DropCreateDatabaseIfModelChanges` class to recognize if the model (schema) has changed before resetting the seed data.</span></span> <span data-ttu-id="62458-191">如果没有对 `Category` 和 `Product` 实体类进行更改，则不会用种子数据重新初始化数据库。</span><span class="sxs-lookup"><span data-stu-id="62458-191">If no changes are made to the `Category` and `Product` entity classes, the database will not be reinitialized with the seed data.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="62458-192">如果希望在每次运行应用程序时重新创建数据库，可以使用 `DropCreateDatabaseAlways` 类，而不是 `DropCreateDatabaseIfModelChanges` 类。</span><span class="sxs-lookup"><span data-stu-id="62458-192">If you wanted the database to be recreated every time you ran the application, you could use the `DropCreateDatabaseAlways` class instead of the `DropCreateDatabaseIfModelChanges` class.</span></span> <span data-ttu-id="62458-193">但对于本系列教程，请使用 `DropCreateDatabaseIfModelChanges` 类。</span><span class="sxs-lookup"><span data-stu-id="62458-193">However for this tutorial series, use the `DropCreateDatabaseIfModelChanges` class.</span></span>

<span data-ttu-id="62458-194">此时，在本教程中，您将拥有一个具有四个新类和一个默认类的*模型*文件夹：</span><span class="sxs-lookup"><span data-stu-id="62458-194">At this point in this tutorial, you will have a *Models* folder with four new classes and one default class:</span></span>

![创建数据访问层-模型文件夹](create_the_data_access_layer/_static/image3.png)

### <a name="configuring-the-application-to-use-the-data-model"></a><span data-ttu-id="62458-196">将应用程序配置为使用数据模型</span><span class="sxs-lookup"><span data-stu-id="62458-196">Configuring the Application to Use the Data Model</span></span>

<span data-ttu-id="62458-197">现在，你已创建表示数据的类，你必须将应用程序配置为使用这些类。</span><span class="sxs-lookup"><span data-stu-id="62458-197">Now that you've created the classes that represent the data, you must configure the application to use the classes.</span></span> <span data-ttu-id="62458-198">在*global.asax*文件中，您将添加初始化模型的代码。</span><span class="sxs-lookup"><span data-stu-id="62458-198">In the *Global.asax* file, you add code that initializes the model.</span></span> <span data-ttu-id="62458-199">*在 web.config 文件中*，添加信息，告诉应用程序将用于存储新数据类所表示的数据的数据库。</span><span class="sxs-lookup"><span data-stu-id="62458-199">In the *Web.config* file you add information that tells the application what database you'll use to store the data that's represented by the new data classes.</span></span> <span data-ttu-id="62458-200">*Global.asax*文件可用于处理应用程序事件或方法。</span><span class="sxs-lookup"><span data-stu-id="62458-200">The *Global.asax* file can be used to handle application events or methods.</span></span> <span data-ttu-id="62458-201">Web.config*文件允许*您控制 ASP.NET Web 应用程序的配置。</span><span class="sxs-lookup"><span data-stu-id="62458-201">The *Web.config* file allows you to control the configuration of your ASP.NET web application.</span></span>

#### <a name="updating-the-globalasax-file"></a><span data-ttu-id="62458-202">更新 global.asax 文件</span><span class="sxs-lookup"><span data-stu-id="62458-202">Updating the Global.asax file</span></span>

<span data-ttu-id="62458-203">若要在应用程序启动时初始化数据模型，您将更新*Global.asax.cs*文件中的 `Application_Start` 处理程序。</span><span class="sxs-lookup"><span data-stu-id="62458-203">To initialize the data models when the application starts, you will update the `Application_Start` handler in the *Global.asax.cs* file.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="62458-204">在解决方案资源管理器中，可以选择*global.asax*文件或*Global.asax.cs*文件来编辑*Global.asax.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="62458-204">In Solution Explorer, you can select either the *Global.asax* file or the *Global.asax.cs* file to edit the *Global.asax.cs* file.</span></span>

1. <span data-ttu-id="62458-205">将以下突出显示的代码添加到*Global.asax.cs*文件中的 `Application_Start` 方法。</span><span class="sxs-lookup"><span data-stu-id="62458-205">Add the following code highlighted in yellow to the `Application_Start` method in the *Global.asax.cs* file.</span></span>   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample5.cs?highlight=9-10,22-23)]

> [!NOTE] 
> 
> <span data-ttu-id="62458-206">浏览器在浏览器中查看此教程系列时，您的浏览器必须支持 HTML5 来查看黄色突出显示的代码。</span><span class="sxs-lookup"><span data-stu-id="62458-206">Your browser must support HTML5 to view the code highlighted in yellow when viewing this tutorial series in a browser.</span></span>

<span data-ttu-id="62458-207">如上面的代码所示，当应用程序启动时，应用程序会指定第一次访问数据时将运行的初始值设定项。</span><span class="sxs-lookup"><span data-stu-id="62458-207">As shown in the above code, when the application starts, the application specifies the initializer that will run during the first time the data is accessed.</span></span> <span data-ttu-id="62458-208">访问 `Database` 对象和 `ProductDatabaseInitializer` 对象需要使用另外两个命名空间。</span><span class="sxs-lookup"><span data-stu-id="62458-208">The two additional namespaces are required to access the `Database` object and the `ProductDatabaseInitializer` object.</span></span>

 <span data-ttu-id="62458-209">修改 Web.config 文件</span><span class="sxs-lookup"><span data-stu-id="62458-209">Modifying the Web.Config File</span></span> 

<span data-ttu-id="62458-210">尽管实体框架 Code First 会在使用种子数据填充数据库时在默认位置为你生成数据库，但将你自己的连接信息添加到你的应用程序可以控制数据库位置。</span><span class="sxs-lookup"><span data-stu-id="62458-210">Although Entity Framework Code First will generate a database for you in a default location when the database is populated with seed data, adding your own connection information to your application gives you control of the database location.</span></span> <span data-ttu-id="62458-211">在项目根目录下，使用应用程序的*web.config*文件中的连接字符串指定此数据库连接。</span><span class="sxs-lookup"><span data-stu-id="62458-211">You specify this database connection using a connection string in the application's *Web.config* file at the root of the project.</span></span> <span data-ttu-id="62458-212">通过添加新的连接字符串，您可以将数据库（*wingtiptoys*）的位置定向到在应用程序的数据目录（*应用程序\_数据*）中生成，而不是在其默认位置。</span><span class="sxs-lookup"><span data-stu-id="62458-212">By adding a new connection string, you can direct the location of the database (*wingtiptoys.mdf*) to be built in the application's data directory (*App\_Data*), rather than its default location.</span></span> <span data-ttu-id="62458-213">进行此更改将允许您在本教程的后面查找并检查数据库文件。</span><span class="sxs-lookup"><span data-stu-id="62458-213">Making this change will allow you to find and inspect the database file later in this tutorial.</span></span>

1. <span data-ttu-id="62458-214">在**解决方案资源管理器**中，找到并打开*web.config 文件。*</span><span class="sxs-lookup"><span data-stu-id="62458-214">In **Solution Explorer**, find and open the *Web.config* file.</span></span>
2. <span data-ttu-id="62458-215">将以黄色突出显示的连接字符串添加到*web.config 文件的*`<connectionStrings>` 节，如下所示：</span><span class="sxs-lookup"><span data-stu-id="62458-215">Add the connection string highlighted in yellow to the `<connectionStrings>` section of the *Web.config* file as follows:</span></span>  

    [!code-xml[Main](create_the_data_access_layer/samples/sample6.xml?highlight=4-7)]

<span data-ttu-id="62458-216">首次运行应用程序时，它将在连接字符串指定的位置生成数据库。</span><span class="sxs-lookup"><span data-stu-id="62458-216">When the application is run for the first time, it will build the database at the location specified by the connection string.</span></span> <span data-ttu-id="62458-217">但在运行应用程序之前，让我们先进行构建。</span><span class="sxs-lookup"><span data-stu-id="62458-217">But before running the application, let's build it first.</span></span>

## <a name="building-the-application"></a><span data-ttu-id="62458-218">生成应用程序</span><span class="sxs-lookup"><span data-stu-id="62458-218">Building the Application</span></span>

<span data-ttu-id="62458-219">若要确保对 Web 应用程序的所有类和更改都有效，应生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="62458-219">To make sure that all the classes and changes to your Web application work, you should build the application.</span></span>

1. <span data-ttu-id="62458-220">从 "**调试**" 菜单中选择 "**生成 WingtipToys**"。</span><span class="sxs-lookup"><span data-stu-id="62458-220">From the **Debug** menu, select **Build WingtipToys**.</span></span>  
 <span data-ttu-id="62458-221">显示 "**输出**" 窗口，如果一切正常，都将看到 "*成功*" 消息。</span><span class="sxs-lookup"><span data-stu-id="62458-221">The **Output** window is displayed, and if all went well, you see a *succeeded* message.</span></span>  

    ![创建数据访问层-输出窗口](create_the_data_access_layer/_static/image4.png)

<span data-ttu-id="62458-223">如果遇到错误，请重新检查以上步骤。</span><span class="sxs-lookup"><span data-stu-id="62458-223">If you run into an error, re-check the above steps.</span></span> <span data-ttu-id="62458-224">"**输出**" 窗口中的信息将指示存在问题的文件，以及文件中需要进行更改的位置。</span><span class="sxs-lookup"><span data-stu-id="62458-224">The information in the **Output** window will indicate which file has a problem and where in the file a change is required.</span></span> <span data-ttu-id="62458-225">此信息使你能够确定需要在你的项目中查看和修复上述哪些步骤。</span><span class="sxs-lookup"><span data-stu-id="62458-225">This information will enable you to determine what part of the above steps need to be reviewed and fixed in your project.</span></span>

## <a name="summary"></a><span data-ttu-id="62458-226">摘要</span><span class="sxs-lookup"><span data-stu-id="62458-226">Summary</span></span>

<span data-ttu-id="62458-227">在本系列教程中，您已创建了数据模型，并添加了将用于初始化和播种数据库的代码。</span><span class="sxs-lookup"><span data-stu-id="62458-227">In this tutorial of the series you have created the data model, as well as, added the code that will be used to initialize and seed the database.</span></span> <span data-ttu-id="62458-228">您还将应用程序配置为在应用程序运行时使用数据模型。</span><span class="sxs-lookup"><span data-stu-id="62458-228">You have also configured the application to use the data models when the application is run.</span></span>

<span data-ttu-id="62458-229">在下一教程中，你将更新 UI，添加导航，并从数据库中检索数据。</span><span class="sxs-lookup"><span data-stu-id="62458-229">In the next tutorial, you'll update the UI, add navigation, and retrieve data from the database.</span></span> <span data-ttu-id="62458-230">这将导致根据你在本教程中创建的实体类来自动创建数据库。</span><span class="sxs-lookup"><span data-stu-id="62458-230">This will result in the database being automatically created based on the entity classes that you created in this tutorial.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="62458-231">其他资源</span><span class="sxs-lookup"><span data-stu-id="62458-231">Additional Resources</span></span>

<span data-ttu-id="62458-232">[实体框架概述](https://msdn.microsoft.com/library/bb399567.aspx) </span><span class="sxs-lookup"><span data-stu-id="62458-232">[Entity Framework Overview](https://msdn.microsoft.com/library/bb399567.aspx) </span></span>  
<span data-ttu-id="62458-233">[ADO.NET 实体框架初学者指南](https://msdn.microsoft.com/data/ee712907) </span><span class="sxs-lookup"><span data-stu-id="62458-233">[Beginner's Guide to the ADO.NET Entity Framework](https://msdn.microsoft.com/data/ee712907) </span></span>  
<span data-ttu-id="62458-234">[实体框架的 Code First 开发](http://www.msteched.com/2010/Europe/DEV212)（视频）</span><span class="sxs-lookup"><span data-stu-id="62458-234">[Code First Development with Entity Framework](http://www.msteched.com/2010/Europe/DEV212) (video)</span></span>   
<span data-ttu-id="62458-235">[Code First 关系流畅 API](https://msdn.microsoft.com/data/hh134698) </span><span class="sxs-lookup"><span data-stu-id="62458-235">[Code First Relationships Fluent API](https://msdn.microsoft.com/data/hh134698) </span></span>  
[<span data-ttu-id="62458-236">Code First 数据批注</span><span class="sxs-lookup"><span data-stu-id="62458-236">Code First Data Annotations</span></span>](https://msdn.microsoft.com/data/gg193958)  
[<span data-ttu-id="62458-237">实体框架的工作效率改进</span><span class="sxs-lookup"><span data-stu-id="62458-237">Productivity Improvements for the Entity Framework</span></span>](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0)

> [!div class="step-by-step"]
> <span data-ttu-id="62458-238">[上一页](create-the-project.md)
> [下一页](ui_and_navigation.md)</span><span class="sxs-lookup"><span data-stu-id="62458-238">[Previous](create-the-project.md)
[Next](ui_and_navigation.md)</span></span>
