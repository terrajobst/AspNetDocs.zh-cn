---
uid: mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
title: 使用业务规则验证构建模型 |Microsoft Docs
author: microsoft
description: 步骤3显示了如何创建可用于查询和更新 NerdDinner 应用程序数据库的模型。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 0bc191b2-4311-479a-a83a-7f1b1c32e6fe
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
msc.type: authoredcontent
ms.openlocfilehash: 6ebf1b71c089229ba9139ff7dc788b8978724046
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78435578"
---
# <a name="build-a-model-with-business-rule-validations"></a><span data-ttu-id="b9086-103">生成具有业务规则验证功能的模型</span><span class="sxs-lookup"><span data-stu-id="b9086-103">Build a Model with Business Rule Validations</span></span>

<span data-ttu-id="b9086-104">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="b9086-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="b9086-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="b9086-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="b9086-106">这是免费的["NerdDinner" 应用程序教程](introducing-the-nerddinner-tutorial.md)的第3步，该教程演示如何使用 ASP.NET MVC 1 构建小型但完整的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="b9086-106">This is step 3 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="b9086-107">步骤3显示了如何创建可用于查询和更新 NerdDinner 应用程序数据库的模型。</span><span class="sxs-lookup"><span data-stu-id="b9086-107">Step 3 shows how to create a model that we can use to both query and update the database for our NerdDinner application.</span></span>
> 
> <span data-ttu-id="b9086-108">如果你使用的是 ASP.NET MVC 3，则建议你遵循[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[Mvc 音乐应用商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程中的入门。</span><span class="sxs-lookup"><span data-stu-id="b9086-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-3-building-the-model"></a><span data-ttu-id="b9086-109">NerdDinner 步骤3：生成模型</span><span class="sxs-lookup"><span data-stu-id="b9086-109">NerdDinner Step 3: Building the Model</span></span>

<span data-ttu-id="b9086-110">在模型视图-控制器框架中，术语 "模型" 是指表示应用程序数据的对象，以及与之集成验证和业务规则的相应域逻辑。</span><span class="sxs-lookup"><span data-stu-id="b9086-110">In a model-view-controller framework the term "model" refers to the objects that represent the data of the application, as well as the corresponding domain logic that integrates validation and business rules with it.</span></span> <span data-ttu-id="b9086-111">模型在很多方面都是基于 MVC 的应用程序的 "核心"，我们稍后将对其进行操作。</span><span class="sxs-lookup"><span data-stu-id="b9086-111">The model is in many ways the "heart" of an MVC-based application, and as we'll see later fundamentally drives the behavior of it.</span></span>

<span data-ttu-id="b9086-112">ASP.NET MVC 框架支持使用任何数据访问技术，开发人员可以从各种丰富的 .NET 数据选项中进行选择，以实现其模型，其中包括： LINQ to Entities、LINQ to SQL、NHibernate、LLBLGen Pro、SubSonic、WilsonORM 或只是原始 ADO。NET Datareader 或数据集。</span><span class="sxs-lookup"><span data-stu-id="b9086-112">The ASP.NET MVC framework supports using any data access technology, and developers can choose from a variety of rich .NET data options to implement their models including: LINQ to Entities, LINQ to SQL, NHibernate, LLBLGen Pro, SubSonic, WilsonORM, or just raw ADO.NET DataReaders or DataSets.</span></span>

<span data-ttu-id="b9086-113">对于我们的 NerdDinner 应用程序，我们将使用 LINQ to SQL 来创建与我们的数据库设计相当紧密的简单模型，并添加一些自定义验证逻辑和业务规则。</span><span class="sxs-lookup"><span data-stu-id="b9086-113">For our NerdDinner application we are going to use LINQ to SQL to create a simple model that corresponds fairly closely to our database design, and adds some custom validation logic and business rules.</span></span> <span data-ttu-id="b9086-114">接下来，我们将实现一个存储库类，以帮助你从应用程序的其余部分抽象掉数据持久性实现，并使我们能够轻松地对其进行单元测试。</span><span class="sxs-lookup"><span data-stu-id="b9086-114">We will then implement a repository class that helps abstract away the data persistence implementation from the rest of the application, and enables us to easily unit test it.</span></span>

### <a name="linq-to-sql"></a><span data-ttu-id="b9086-115">LINQ to SQL</span><span class="sxs-lookup"><span data-stu-id="b9086-115">LINQ to SQL</span></span>

<span data-ttu-id="b9086-116">LINQ to SQL 是 .NET 3.5 中附带的 ORM （对象关系映射器）。</span><span class="sxs-lookup"><span data-stu-id="b9086-116">LINQ to SQL is an ORM (object relational mapper) that ships as part of .NET 3.5.</span></span>

<span data-ttu-id="b9086-117">LINQ to SQL 提供了一种简单的方法，将数据库表映射到我们可以对其进行编码的 .NET 类。</span><span class="sxs-lookup"><span data-stu-id="b9086-117">LINQ to SQL provides an easy way to map database tables to .NET classes we can code against.</span></span> <span data-ttu-id="b9086-118">对于我们的 NerdDinner 应用程序，我们将使用它将数据库中的就和 RSVP 表映射到晚餐和 RSVP 类。</span><span class="sxs-lookup"><span data-stu-id="b9086-118">For our NerdDinner application we'll use it to map the Dinners and RSVP tables within our database to Dinner and RSVP classes.</span></span> <span data-ttu-id="b9086-119">就表和 RSVP 表中的列将与晚餐和 RSVP 类的属性相对应。</span><span class="sxs-lookup"><span data-stu-id="b9086-119">The columns of the Dinners and RSVP tables will correspond to properties on the Dinner and RSVP classes.</span></span> <span data-ttu-id="b9086-120">每个晚餐和 RSVP 对象将代表数据库中就表或 RSVP 表中的一行。</span><span class="sxs-lookup"><span data-stu-id="b9086-120">Each Dinner and RSVP object will represent a separate row within the Dinners or RSVP tables in the database.</span></span>

<span data-ttu-id="b9086-121">LINQ to SQL 使我们不必手动构建 SQL 语句来检索和更新包含数据库数据的晚餐和 RSVP 对象。</span><span class="sxs-lookup"><span data-stu-id="b9086-121">LINQ to SQL allows us to avoid having to manually construct SQL statements to retrieve and update Dinner and RSVP objects with database data.</span></span> <span data-ttu-id="b9086-122">相反，我们将定义晚餐和 RSVP 类，它们如何映射到数据库以及它们之间的关系。</span><span class="sxs-lookup"><span data-stu-id="b9086-122">Instead, we'll define the Dinner and RSVP classes, how they map to/from the database, and the relationships between them.</span></span> <span data-ttu-id="b9086-123">接下来，LINQ to SQL 将负责生成合适的 SQL 执行逻辑以便在运行时使用它们。</span><span class="sxs-lookup"><span data-stu-id="b9086-123">LINQ to SQL will then takes care of generating the appropriate SQL execution logic to use at runtime when we interact and use them.</span></span>

<span data-ttu-id="b9086-124">我们可以使用 VB 中的 LINQ 语言支持， C#并编写可从数据库中检索晚餐和 RSVP 对象的可表达性查询。</span><span class="sxs-lookup"><span data-stu-id="b9086-124">We can use the LINQ language support within VB and C# to write expressive queries that retrieve Dinner and RSVP objects from the database.</span></span> <span data-ttu-id="b9086-125">这可以最大程度地减少需要编写的数据代码量，并使我们能够构建真正干净的应用程序。</span><span class="sxs-lookup"><span data-stu-id="b9086-125">This minimizes the amount of data code we need to write, and allows us to build really clean applications.</span></span>

### <a name="adding-linq-to-sql-classes-to-our-project"></a><span data-ttu-id="b9086-126">向项目添加 LINQ to SQL 类</span><span class="sxs-lookup"><span data-stu-id="b9086-126">Adding LINQ to SQL Classes to our project</span></span>

<span data-ttu-id="b9086-127">首先，右键单击项目中的 "模型" 文件夹，然后选择 "**添加-&gt;新项**" 菜单命令：</span><span class="sxs-lookup"><span data-stu-id="b9086-127">We'll begin by right-clicking on the "Models" folder within our project, and select the **Add-&gt;New Item** menu command:</span></span>

![](build-a-model-with-business-rule-validations/_static/image1.png)

<span data-ttu-id="b9086-128">这会显示 "添加新项" 对话框。</span><span class="sxs-lookup"><span data-stu-id="b9086-128">This will bring up the "Add New Item" dialog.</span></span> <span data-ttu-id="b9086-129">我们将按 "数据" 类别进行筛选，并选择其中的 "LINQ to SQL 类" 模板：</span><span class="sxs-lookup"><span data-stu-id="b9086-129">We'll filter by the "Data" category and select the "LINQ to SQL Classes" template within it:</span></span>

![](build-a-model-with-business-rule-validations/_static/image2.png)

<span data-ttu-id="b9086-130">我们会将项目命名为 "NerdDinner"，并单击 "添加" 按钮。</span><span class="sxs-lookup"><span data-stu-id="b9086-130">We'll name the item "NerdDinner" and click the "Add" button.</span></span> <span data-ttu-id="b9086-131">Visual Studio 将在我们的 \Models 目录下添加一个 NerdDinner 文件，然后打开 LINQ to SQL 对象关系设计器：</span><span class="sxs-lookup"><span data-stu-id="b9086-131">Visual Studio will add a NerdDinner.dbml file under our \Models directory, and then open the LINQ to SQL object relational designer:</span></span>

![](build-a-model-with-business-rule-validations/_static/image3.png)

### <a name="creating-data-model-classes-with-linq-to-sql"></a><span data-ttu-id="b9086-132">创建具有 LINQ to SQL 的数据模型类</span><span class="sxs-lookup"><span data-stu-id="b9086-132">Creating Data Model Classes with LINQ to SQL</span></span>

<span data-ttu-id="b9086-133">LINQ to SQL 使我们可以从现有的数据库架构中快速创建数据模型类。</span><span class="sxs-lookup"><span data-stu-id="b9086-133">LINQ to SQL enables us to quickly create data model classes from existing database schema.</span></span> <span data-ttu-id="b9086-134">为此，我们将在服务器资源管理器中打开 NerdDinner 数据库，并选择要在其中进行建模的表：</span><span class="sxs-lookup"><span data-stu-id="b9086-134">To-do this we'll open the NerdDinner database in the Server Explorer, and select the Tables we want to model in it:</span></span>

![](build-a-model-with-business-rule-validations/_static/image4.png)

<span data-ttu-id="b9086-135">然后，可以将这些表拖放到 LINQ to SQL 设计器图面上。</span><span class="sxs-lookup"><span data-stu-id="b9086-135">We can then drag the tables onto the LINQ to SQL designer surface.</span></span> <span data-ttu-id="b9086-136">如果执行此操作 LINQ to SQL 将使用表的架构（带有映射到数据库表列的类属性）自动创建晚餐和 RSVP 类：</span><span class="sxs-lookup"><span data-stu-id="b9086-136">When we do this LINQ to SQL will automatically create Dinner and RSVP classes using the schema of the tables (with class properties that map to the database table columns):</span></span>

![](build-a-model-with-business-rule-validations/_static/image5.png)

<span data-ttu-id="b9086-137">默认情况下，在基于数据库架构创建类时，LINQ to SQL 设计器会自动 "为" 表和列名。</span><span class="sxs-lookup"><span data-stu-id="b9086-137">By default the LINQ to SQL designer automatically "pluralizes" table and column names when it creates classes based on a database schema.</span></span> <span data-ttu-id="b9086-138">例如，上面示例中的 "就" 表导致了 "晚餐" 类。</span><span class="sxs-lookup"><span data-stu-id="b9086-138">For example: the "Dinners" table in our example above resulted in a "Dinner" class.</span></span> <span data-ttu-id="b9086-139">此类命名有助于使模型与 .NET 命名约定保持一致，并且通常会发现设计器很方便地解决这一问题（尤其是在添加大量表时）。</span><span class="sxs-lookup"><span data-stu-id="b9086-139">This class naming helps make our models consistent with .NET naming conventions, and I usually find that having the designer fix this up convenient (especially when adding lots of tables).</span></span> <span data-ttu-id="b9086-140">不过，如果您不喜欢设计器生成的类或属性的名称，您始终可以重写它并将其更改为任何所需的名称。</span><span class="sxs-lookup"><span data-stu-id="b9086-140">If you don't like the name of a class or property that the designer generates, though, you can always override it and change it to any name you want.</span></span> <span data-ttu-id="b9086-141">为此，可以在设计器中编辑实体/属性名称，也可以通过属性网格修改它。</span><span class="sxs-lookup"><span data-stu-id="b9086-141">You can do this either by editing the entity/property name in-line within the designer or by modifying it via the property grid.</span></span>

<span data-ttu-id="b9086-142">默认情况下，LINQ to SQL 设计器还会检查表的主键/外键关系，并根据它们在创建的不同模型类之间自动创建默认的 "关系关联"。</span><span class="sxs-lookup"><span data-stu-id="b9086-142">By default the LINQ to SQL designer also inspects the primary key/foreign key relationships of the tables, and based on them automatically creates default "relationship associations" between the different model classes it creates.</span></span> <span data-ttu-id="b9086-143">例如，将就和 RSVP 表拖放到 LINQ to SQL 设计器上时，这两个表之间的一对多关系关联是根据 RSVP 表具有就表的外键得出的，这是由设计器）：</span><span class="sxs-lookup"><span data-stu-id="b9086-143">For example, when we dragged the Dinners and RSVP tables onto the LINQ to SQL designer a one-to-many relationship association between the two was inferred based on the fact that the RSVP table had a foreign-key to the Dinners table (this is indicated by the arrow in the designer):</span></span>

![](build-a-model-with-business-rule-validations/_static/image6.png)

<span data-ttu-id="b9086-144">上述关联将导致 LINQ to SQL 将强类型的 "晚餐" 属性添加到 RSVP 类，开发人员可以使用该属性来访问与给定 RSVP 相关的晚餐。</span><span class="sxs-lookup"><span data-stu-id="b9086-144">The above association will cause LINQ to SQL to add a strongly typed "Dinner" property to the RSVP class that developers can use to access the Dinner associated with a given RSVP.</span></span> <span data-ttu-id="b9086-145">它还会导致晚餐类具有一个 "RSVPs" 集合属性，使开发人员能够检索和更新与特定晚餐关联的 RSVP 对象。</span><span class="sxs-lookup"><span data-stu-id="b9086-145">It will also cause the Dinner class to have a "RSVPs" collection property that enables developers to retrieve and update RSVP objects associated with a particular Dinner.</span></span>

<span data-ttu-id="b9086-146">在下面，你可以在 Visual Studio 中看到一个 intellisense 示例，当我们创建新的 RSVP 对象并将其添加到晚餐的 RSVPs 集合时。</span><span class="sxs-lookup"><span data-stu-id="b9086-146">Below you can see an example of intellisense within Visual Studio when we create a new RSVP object and add it to a Dinner's RSVPs collection.</span></span> <span data-ttu-id="b9086-147">请注意 LINQ to SQL 如何自动在晚餐对象上添加 "RSVPs" 集合：</span><span class="sxs-lookup"><span data-stu-id="b9086-147">Notice how LINQ to SQL automatically added a "RSVPs" collection on the Dinner object:</span></span>

![](build-a-model-with-business-rule-validations/_static/image7.png)

<span data-ttu-id="b9086-148">通过将 RSVP 对象添加到晚餐的 RSVPs 集合中，我们会告诉 LINQ to SQL 在我们的数据库中关联晚餐和 RSVP 行之间的外键关系：</span><span class="sxs-lookup"><span data-stu-id="b9086-148">By adding the RSVP object to the Dinner's RSVPs collection we are telling LINQ to SQL to associate a foreign-key relationship between the Dinner and the RSVP row in our database:</span></span>

![](build-a-model-with-business-rule-validations/_static/image8.png)

<span data-ttu-id="b9086-149">如果您不喜欢设计器如何建模或命名表关联，则可以重写它。</span><span class="sxs-lookup"><span data-stu-id="b9086-149">If you don't like how the designer has modeled or named a table association, you can override it.</span></span> <span data-ttu-id="b9086-150">只需单击设计器中的 "关联" 箭头并通过属性网格访问其属性，即可重命名、删除或修改它。</span><span class="sxs-lookup"><span data-stu-id="b9086-150">Just click on the association arrow within the designer and access its properties via the property grid to rename, delete or modify it.</span></span> <span data-ttu-id="b9086-151">但对于我们的 NerdDinner 应用程序，默认关联规则适用于正在生成的数据模型类，并且我们只使用默认行为。</span><span class="sxs-lookup"><span data-stu-id="b9086-151">For our NerdDinner application, though, the default association rules work well for the data model classes we are building and we can just use the default behavior.</span></span>

### <a name="nerddinnerdatacontext-class"></a><span data-ttu-id="b9086-152">NerdDinnerDataContext 类</span><span class="sxs-lookup"><span data-stu-id="b9086-152">NerdDinnerDataContext Class</span></span>

<span data-ttu-id="b9086-153">Visual Studio 将自动创建表示使用 LINQ to SQL 设计器定义的模型和数据库关系的 .NET 类。</span><span class="sxs-lookup"><span data-stu-id="b9086-153">Visual Studio will automatically create .NET classes that represent the models and database relationships defined using the LINQ to SQL designer.</span></span> <span data-ttu-id="b9086-154">还为添加到解决方案中的每个 LINQ to SQL 设计器文件生成一个 LINQ to SQL DataContext 类。</span><span class="sxs-lookup"><span data-stu-id="b9086-154">A LINQ to SQL DataContext class is also generated for each LINQ to SQL designer file added to the solution.</span></span> <span data-ttu-id="b9086-155">由于我们将 LINQ to SQL 类项命名为 "NerdDinner"，因此创建的 DataContext 类将称为 "NerdDinnerDataContext"。</span><span class="sxs-lookup"><span data-stu-id="b9086-155">Because we named our LINQ to SQL class item "NerdDinner", the DataContext class created will be called "NerdDinnerDataContext".</span></span> <span data-ttu-id="b9086-156">此 NerdDinnerDataContext 类是我们将与数据库进行交互的主要方式。</span><span class="sxs-lookup"><span data-stu-id="b9086-156">This NerdDinnerDataContext class is the primary way we will interact with the database.</span></span>

<span data-ttu-id="b9086-157">我们的 NerdDinnerDataContext 类公开了两个属性-"就" 和 "RSVPs"-表示在数据库中建模的两个表。</span><span class="sxs-lookup"><span data-stu-id="b9086-157">Our NerdDinnerDataContext class exposes two properties - "Dinners" and "RSVPs" - that represent the two tables we modeled within the database.</span></span> <span data-ttu-id="b9086-158">我们可以使用C#编写针对这些属性的 LINQ 查询，以便从数据库中查询和检索晚餐和 RSVP 对象。</span><span class="sxs-lookup"><span data-stu-id="b9086-158">We can use C# to write LINQ queries against those properties to query and retrieve Dinner and RSVP objects from the database.</span></span>

<span data-ttu-id="b9086-159">下面的代码演示如何实例化 NerdDinnerDataContext 对象，并对其执行 LINQ 查询以获取将来发生的就序列。</span><span class="sxs-lookup"><span data-stu-id="b9086-159">The following code demonstrates how to instantiate a NerdDinnerDataContext object and perform a LINQ query against it to obtain a sequence of Dinners that occur in the future.</span></span> <span data-ttu-id="b9086-160">在编写 LINQ 查询时，Visual Studio 提供完整的 intellisense，从它返回的对象是强类型化的，并且还支持 intellisense：</span><span class="sxs-lookup"><span data-stu-id="b9086-160">Visual Studio provides full intellisense when writing the LINQ query, and the objects returned from it are strongly-typed and also support intellisense:</span></span>

![](build-a-model-with-business-rule-validations/_static/image9.png)

<span data-ttu-id="b9086-161">除了允许我们查询晚餐和 RSVP 对象外，NerdDinnerDataContext 还会自动跟踪我们通过它检索到的晚餐和 RSVP 对象所做的任何更改。</span><span class="sxs-lookup"><span data-stu-id="b9086-161">In addition to allowing us to query for Dinner and RSVP objects, a NerdDinnerDataContext also automatically tracks any changes we subsequently make to the Dinner and RSVP objects we retrieve through it.</span></span> <span data-ttu-id="b9086-162">使用此功能可以轻松地将更改保存回数据库-无需编写任何显式的 SQL 更新代码。</span><span class="sxs-lookup"><span data-stu-id="b9086-162">We can use this functionality to easily save the changes back to the database - without having to write any explicit SQL update code.</span></span>

<span data-ttu-id="b9086-163">例如，下面的代码演示了如何使用 LINQ 查询从数据库检索单个晚餐对象，更新两个晚餐属性，然后将更改保存回数据库：</span><span class="sxs-lookup"><span data-stu-id="b9086-163">For example, the code below demonstrates how to use a LINQ query to retrieve a single Dinner object from the database, update two of the Dinner properties, and then save the changes back to the database:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample1.cs)]

<span data-ttu-id="b9086-164">上面代码中的 NerdDinnerDataContext 对象自动跟踪对其检索到的晚餐对象所做的属性更改。</span><span class="sxs-lookup"><span data-stu-id="b9086-164">The NerdDinnerDataContext object in the code above automatically tracked the property changes made to the Dinner object we retrieved from it.</span></span> <span data-ttu-id="b9086-165">当我们调用了 "SubmitChanges （）" 方法时，它会对数据库执行适当的 SQL "UPDATE" 语句，以将更新后的值保留回去。</span><span class="sxs-lookup"><span data-stu-id="b9086-165">When we called the "SubmitChanges()" method, it will execute an appropriate SQL "UPDATE" statement to the database to persist the updated values back.</span></span>

### <a name="creating-a-dinnerrepository-class"></a><span data-ttu-id="b9086-166">创建 DinnerRepository 类</span><span class="sxs-lookup"><span data-stu-id="b9086-166">Creating a DinnerRepository Class</span></span>

<span data-ttu-id="b9086-167">对于小型应用程序，有时可以让控制器直接处理 LINQ to SQL DataContext 类，并在控制器中嵌入 LINQ 查询。</span><span class="sxs-lookup"><span data-stu-id="b9086-167">For small applications it is sometimes fine to have Controllers work directly against a LINQ to SQL DataContext class, and embed LINQ queries within the Controllers.</span></span> <span data-ttu-id="b9086-168">然而，随着应用程序变得更大，维护和测试此方法会变得很繁琐。</span><span class="sxs-lookup"><span data-stu-id="b9086-168">As applications get larger, though, this approach becomes cumbersome to maintain and test.</span></span> <span data-ttu-id="b9086-169">它还会导致我们在多个位置复制相同的 LINQ 查询。</span><span class="sxs-lookup"><span data-stu-id="b9086-169">It can also lead to us duplicating the same LINQ queries in multiple places.</span></span>

<span data-ttu-id="b9086-170">可以使应用程序更易于维护和测试的一种方法是使用 "存储库" 模式。</span><span class="sxs-lookup"><span data-stu-id="b9086-170">One approach that can make applications easier to maintain and test is to use a "repository" pattern.</span></span> <span data-ttu-id="b9086-171">存储库类有助于封装数据查询和持久性逻辑，并从应用程序中提取数据持久性的实现细节。</span><span class="sxs-lookup"><span data-stu-id="b9086-171">A repository class helps encapsulate data querying and persistence logic, and abstracts away the implementation details of the data persistence from the application.</span></span> <span data-ttu-id="b9086-172">除了使应用程序代码更整洁，使用存储库模式还可以更轻松地在将来更改数据存储实现，并且它有助于简化应用程序的单元测试，而无需实际数据库。</span><span class="sxs-lookup"><span data-stu-id="b9086-172">In addition to making application code cleaner, using a repository pattern can make it easier to change data storage implementations in the future, and it can help facilitate unit testing an application without requiring a real database.</span></span>

<span data-ttu-id="b9086-173">对于我们的 NerdDinner 应用程序，我们将使用以下签名定义一个 DinnerRepository 类：</span><span class="sxs-lookup"><span data-stu-id="b9086-173">For our NerdDinner application we'll define a DinnerRepository class with the below signature:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample2.cs)]

<span data-ttu-id="b9086-174">*注意：本章稍后将从此类中提取 IDinnerRepository 接口，并在控制器上启用依赖项注入。不过，从开始，我们将简单直接使用 DinnerRepository 类。*</span><span class="sxs-lookup"><span data-stu-id="b9086-174">*Note: Later in this chapter we'll extract an IDinnerRepository interface from this class and enable dependency injection with it on our Controllers. To begin with, though, we are going to start simple and just work directly with the DinnerRepository class.*</span></span>

<span data-ttu-id="b9086-175">若要实现此类，请右键单击 "模型" 文件夹，然后选择 "**添加-&gt;新项**" 菜单命令。</span><span class="sxs-lookup"><span data-stu-id="b9086-175">To implement this class we'll right-click on our "Models" folder and choose the **Add-&gt;New Item** menu command.</span></span> <span data-ttu-id="b9086-176">在 "添加新项" 对话框中，选择 "类" 模板，并将文件命名为 "DinnerRepository.cs"：</span><span class="sxs-lookup"><span data-stu-id="b9086-176">Within the "Add New Item" dialog we'll select the "Class" template and name the file "DinnerRepository.cs":</span></span>

![](build-a-model-with-business-rule-validations/_static/image10.png)

<span data-ttu-id="b9086-177">然后，可以使用以下代码实现 DinnerRepository 类：</span><span class="sxs-lookup"><span data-stu-id="b9086-177">We can then implement our DinnerRepository class using the code below:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample3.cs)]

### <a name="retrieving-updating-inserting-and-deleting-using-the-dinnerrepository-class"></a><span data-ttu-id="b9086-178">使用 DinnerRepository 类检索、更新、插入和删除</span><span class="sxs-lookup"><span data-stu-id="b9086-178">Retrieving, Updating, Inserting and Deleting using the DinnerRepository class</span></span>

<span data-ttu-id="b9086-179">现在，我们已经创建了 DinnerRepository 类，接下来让我们看看一些代码示例，这些示例演示了我们可以使用它完成的常见任务：</span><span class="sxs-lookup"><span data-stu-id="b9086-179">Now that we've created our DinnerRepository class, let's look at a few code examples that demonstrate common tasks we can do with it:</span></span>

#### <a name="querying-examples"></a><span data-ttu-id="b9086-180">查询示例</span><span class="sxs-lookup"><span data-stu-id="b9086-180">Querying Examples</span></span>

<span data-ttu-id="b9086-181">以下代码使用 DinnerID 值检索单个晚宴：</span><span class="sxs-lookup"><span data-stu-id="b9086-181">The code below retrieves a single Dinner using the DinnerID value:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample4.cs)]

<span data-ttu-id="b9086-182">下面的代码检索所有即将发布的就和循环：</span><span class="sxs-lookup"><span data-stu-id="b9086-182">The code below retrieves all upcoming dinners and loops over them:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample5.cs)]

#### <a name="insert-and-update-examples"></a><span data-ttu-id="b9086-183">插入和更新示例</span><span class="sxs-lookup"><span data-stu-id="b9086-183">Insert and Update Examples</span></span>

<span data-ttu-id="b9086-184">下面的代码演示如何添加两个新的就。</span><span class="sxs-lookup"><span data-stu-id="b9086-184">The code below demonstrates adding two new dinners.</span></span> <span data-ttu-id="b9086-185">在对存储库进行添加/修改之前，不会将其添加到数据库中。</span><span class="sxs-lookup"><span data-stu-id="b9086-185">Additions/modifications to the repository aren't committed to the database until the "Save()" method is called on it.</span></span> <span data-ttu-id="b9086-186">LINQ to SQL 自动包装数据库事务中的所有更改-因此，在存储库保存时，所有更改都将发生，或者都不执行更改：</span><span class="sxs-lookup"><span data-stu-id="b9086-186">LINQ to SQL automatically wraps all changes in a database transaction – so either all changes happen or none of them do when our repository saves:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample6.cs)]

<span data-ttu-id="b9086-187">下面的代码检索现有晚餐对象，并修改其中的两个属性。</span><span class="sxs-lookup"><span data-stu-id="b9086-187">The code below retrieves an existing Dinner object, and modifies two properties on it.</span></span> <span data-ttu-id="b9086-188">在我们的存储库中调用 "Save （）" 方法时，会将更改提交回数据库：</span><span class="sxs-lookup"><span data-stu-id="b9086-188">The changes are committed back to the database when the "Save()" method is called on our repository:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample7.cs)]

<span data-ttu-id="b9086-189">下面的代码检索晚餐，然后向其添加 RSVP。</span><span class="sxs-lookup"><span data-stu-id="b9086-189">The code below retrieves a dinner and then adds an RSVP to it.</span></span> <span data-ttu-id="b9086-190">它使用 LINQ to SQL 为我们创建的晚餐对象上的 RSVPs 集合来完成此工作（因为数据库中的两者之间存在主键/外键关系）。</span><span class="sxs-lookup"><span data-stu-id="b9086-190">It does this using the RSVPs collection on the Dinner object that LINQ to SQL created for us (because there is a primary-key/foreign-key relationship between the two in the database).</span></span> <span data-ttu-id="b9086-191">当在存储库中调用 "Save （）" 方法时，此更改将作为新的 RSVP 表行保留回数据库：</span><span class="sxs-lookup"><span data-stu-id="b9086-191">This change is persisted back to the database as a new RSVP table row when the "Save()" method is called on the repository:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample8.cs)]

#### <a name="delete-example"></a><span data-ttu-id="b9086-192">删除示例</span><span class="sxs-lookup"><span data-stu-id="b9086-192">Delete Example</span></span>

<span data-ttu-id="b9086-193">下面的代码检索现有晚餐对象，然后将其标记为已删除。</span><span class="sxs-lookup"><span data-stu-id="b9086-193">The code below retrieves an existing Dinner object, and then marks it to be deleted.</span></span> <span data-ttu-id="b9086-194">在存储库中调用 "Save （）" 方法时，它会将删除提交回数据库：</span><span class="sxs-lookup"><span data-stu-id="b9086-194">When the "Save()" method is called on the repository it will commit the delete back to the database:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample9.cs)]

### <a name="integrating-validation-and-business-rule-logic-with-model-classes"></a><span data-ttu-id="b9086-195">将验证和业务规则逻辑与模型类集成</span><span class="sxs-lookup"><span data-stu-id="b9086-195">Integrating Validation and Business Rule Logic with Model Classes</span></span>

<span data-ttu-id="b9086-196">集成验证和业务规则逻辑是适用于数据的任何应用程序的关键部分。</span><span class="sxs-lookup"><span data-stu-id="b9086-196">Integrating validation and business rule logic is a key part of any application that works with data.</span></span>

#### <a name="schema-validation"></a><span data-ttu-id="b9086-197">架构验证</span><span class="sxs-lookup"><span data-stu-id="b9086-197">Schema Validation</span></span>

<span data-ttu-id="b9086-198">当使用 LINQ to SQL 设计器定义模型类时，数据模型类中的属性的数据类型对应于数据库表的数据类型。</span><span class="sxs-lookup"><span data-stu-id="b9086-198">When model classes are defined using the LINQ to SQL designer, the datatypes of the properties in the data model classes correspond to the datatypes of the database table.</span></span> <span data-ttu-id="b9086-199">例如：如果就表中的 "EventDate" 列是 "datetime"，则 LINQ to SQL 创建的数据模型类将是 "DateTime" 类型（这是一种内置的 .NET 数据类型）。</span><span class="sxs-lookup"><span data-stu-id="b9086-199">For example: if the "EventDate" column in the Dinners table is a "datetime", the data model class created by LINQ to SQL will be of type "DateTime" (which is a built-in .NET datatype).</span></span> <span data-ttu-id="b9086-200">这意味着，如果您尝试从代码向代码分配一个整数或布尔值，将会出现编译错误，如果在运行时尝试将无效字符串类型隐式转换为它，则会自动引发错误。</span><span class="sxs-lookup"><span data-stu-id="b9086-200">This means you will get compile errors if you attempt to assign an integer or boolean to it from code, and it will raise an error automatically if you attempt to implicitly convert a non-valid string type to it at runtime.</span></span>

<span data-ttu-id="b9086-201">使用字符串时，LINQ to SQL 还将自动为你处理转义 SQL 值，这有助于在使用它时防止出现 SQL 注入式攻击。</span><span class="sxs-lookup"><span data-stu-id="b9086-201">LINQ to SQL will also automatically handles escaping SQL values for you when using strings - which helps protect you against SQL injection attacks when using it.</span></span>

#### <a name="validation-and-business-rule-logic"></a><span data-ttu-id="b9086-202">验证和业务规则逻辑</span><span class="sxs-lookup"><span data-stu-id="b9086-202">Validation and Business Rule Logic</span></span>

<span data-ttu-id="b9086-203">架构验证在第一步中非常有用，但这很少。</span><span class="sxs-lookup"><span data-stu-id="b9086-203">Schema validation is useful as a first step, but is rarely sufficient.</span></span> <span data-ttu-id="b9086-204">大多数现实情况下，都需要能够指定更丰富的验证逻辑，该逻辑可跨多个属性、执行代码，并经常识别模型的状态（例如：是在/updated/deleted 中创建，还是在特定于域的状态，如 "已存档"）。</span><span class="sxs-lookup"><span data-stu-id="b9086-204">Most real-world scenarios require the ability to specify richer validation logic that can span multiple properties, execute code, and often have awareness of a model's state (for example: is it being created /updated/deleted, or within a domain-specific state like "archived").</span></span> <span data-ttu-id="b9086-205">有多种不同的模式和框架可用于定义模型类并将其应用于模型类，并且有多个基于 .NET 的框架可用于帮助解决此问题。</span><span class="sxs-lookup"><span data-stu-id="b9086-205">There are a variety of different patterns and frameworks that can be used to define and apply validation rules to model classes, and there are several .NET based frameworks out there that can be used to help with this.</span></span> <span data-ttu-id="b9086-206">在 ASP.NET MVC 应用程序中，可以使用它们中的任何一个。</span><span class="sxs-lookup"><span data-stu-id="b9086-206">You can use pretty much any of them within ASP.NET MVC applications.</span></span>

<span data-ttu-id="b9086-207">为了实现 NerdDinner 应用程序的目的，我们将使用一个相对简单的直连模式，在此模式下，我们将在晚餐模型对象上公开 IsValid 属性和 GetRuleViolations （）方法。</span><span class="sxs-lookup"><span data-stu-id="b9086-207">For the purposes of our NerdDinner application, we'll use a relatively simple and straight-forward pattern where we expose an IsValid property and a GetRuleViolations() method on our Dinner model object.</span></span> <span data-ttu-id="b9086-208">IsValid 属性将返回 true 或 false，具体取决于验证和业务规则是否都有效。</span><span class="sxs-lookup"><span data-stu-id="b9086-208">The IsValid property will return true or false depending on whether the validation and business rules are all valid.</span></span> <span data-ttu-id="b9086-209">GetRuleViolations （）方法将返回任何规则错误的列表。</span><span class="sxs-lookup"><span data-stu-id="b9086-209">The GetRuleViolations() method will return a list of any rule errors.</span></span>

<span data-ttu-id="b9086-210">我们将通过向项目中添加 "partial 类"，为晚餐模型实现 IsValid 和 GetRuleViolations （）。</span><span class="sxs-lookup"><span data-stu-id="b9086-210">We'll implement IsValid and GetRuleViolations() for our Dinner model by adding a "partial class" to our project.</span></span> <span data-ttu-id="b9086-211">分部类可用于将方法/属性/事件添加到 VS 设计器所维护的类（例如，由 LINQ to SQL 设计器生成的晚餐类），并有助于避免使用我们的代码以免混乱该工具。</span><span class="sxs-lookup"><span data-stu-id="b9086-211">Partial classes can be used to add methods/properties/events to classes maintained by a VS designer (like the Dinner class generated by the LINQ to SQL designer) and help avoid the tool from messing with our code.</span></span> <span data-ttu-id="b9086-212">可以通过右键单击 \Models 文件夹，然后选择 "添加新项" 菜单命令向项目中添加一个新的分部类。</span><span class="sxs-lookup"><span data-stu-id="b9086-212">We can add a new partial class to our project by right-clicking on the \Models folder, and then select the "Add New Item" menu command.</span></span> <span data-ttu-id="b9086-213">然后，可以在 "添加新项" 对话框中选择 "类" 模板，并将其命名为 Dinner.cs。</span><span class="sxs-lookup"><span data-stu-id="b9086-213">We can then choose the "Class" template within the "Add New Item" dialog and name it Dinner.cs.</span></span>

![](build-a-model-with-business-rule-validations/_static/image11.png)

<span data-ttu-id="b9086-214">单击 "添加" 按钮会将 Dinner.cs 文件添加到项目中，并在 IDE 中打开它。</span><span class="sxs-lookup"><span data-stu-id="b9086-214">Clicking the "Add" button will add a Dinner.cs file to our project and open it within the IDE.</span></span> <span data-ttu-id="b9086-215">然后，可以使用以下代码实现基本规则/验证强制框架：</span><span class="sxs-lookup"><span data-stu-id="b9086-215">We can then implement a basic rule/validation enforcement framework using the below code:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample10.cs)]

<span data-ttu-id="b9086-216">有关上述代码的几点说明：</span><span class="sxs-lookup"><span data-stu-id="b9086-216">A few notes about the above code:</span></span>

- <span data-ttu-id="b9086-217">晚餐类以 "partial" 关键字开头-这意味着，其中包含的代码将与 LINQ to SQL 设计器生成/维护并编译为单一类的类结合使用。</span><span class="sxs-lookup"><span data-stu-id="b9086-217">The Dinner class is prefaced with a "partial" keyword – which means the code contained within it will be combined with the class generated/maintained by the LINQ to SQL designer and compiled into a single class.</span></span>
- <span data-ttu-id="b9086-218">RuleViolation 类是一个帮助器类，它将添加到项目中，以允许我们提供有关规则冲突的更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="b9086-218">The RuleViolation class is a helper class we'll add to the project that allows us to provide more details about a rule violation.</span></span>
- <span data-ttu-id="b9086-219">GetRuleViolations （）方法会导致对验证和业务规则进行评估（我们将很快实现这些规则）。</span><span class="sxs-lookup"><span data-stu-id="b9086-219">The Dinner.GetRuleViolations() method causes our validation and business rules to be evaluated (we'll implement them shortly).</span></span> <span data-ttu-id="b9086-220">然后返回一系列 RuleViolation 对象，这些对象提供有关任何规则错误的更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="b9086-220">It then returns back a sequence of RuleViolation objects that provide more details about any rule errors.</span></span>
- <span data-ttu-id="b9086-221">"晚餐" 属性提供了一个方便的帮助程序属性，该属性指示晚餐对象是否具有任何活动的 RuleViolations。</span><span class="sxs-lookup"><span data-stu-id="b9086-221">The Dinner.IsValid property provides a convenient helper property that indicates whether the Dinner object has any active RuleViolations.</span></span> <span data-ttu-id="b9086-222">开发人员可随时使用晚餐对象进行主动检查（不会引发异常）。</span><span class="sxs-lookup"><span data-stu-id="b9086-222">It can be proactively checked by a developer using the Dinner object at anytime (and does not raise an exception).</span></span>
- <span data-ttu-id="b9086-223">OnValidate （）分部方法是 LINQ to SQL 提供的挂钩，使我们能够在该数据库中保留晚餐对象时收到通知。</span><span class="sxs-lookup"><span data-stu-id="b9086-223">The Dinner.OnValidate() partial method is a hook that LINQ to SQL provides that allows us to be notified anytime the Dinner object is about to be persisted within the database.</span></span> <span data-ttu-id="b9086-224">上述 OnValidate （）实现可确保晚餐在保存前没有 RuleViolations。</span><span class="sxs-lookup"><span data-stu-id="b9086-224">Our OnValidate() implementation above ensures that the Dinner has no RuleViolations before it is saved.</span></span> <span data-ttu-id="b9086-225">如果它处于无效状态，则会引发异常，这将导致 LINQ to SQL 中止该事务。</span><span class="sxs-lookup"><span data-stu-id="b9086-225">If it is in an invalid state it raises an exception, which will cause LINQ to SQL to abort the transaction.</span></span>

<span data-ttu-id="b9086-226">此方法提供了一个简单的框架，可将验证和业务规则集成到其中。</span><span class="sxs-lookup"><span data-stu-id="b9086-226">This approach provides a simple framework that we can integrate validation and business rules into.</span></span> <span data-ttu-id="b9086-227">现在，让我们将以下规则添加到 GetRuleViolations （）方法：</span><span class="sxs-lookup"><span data-stu-id="b9086-227">For now let's add the below rules to our GetRuleViolations() method:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample11.cs)]

<span data-ttu-id="b9086-228">我们使用的C# "yield return" 功能返回任何 RuleViolations 的序列。</span><span class="sxs-lookup"><span data-stu-id="b9086-228">We are using the "yield return" feature of C# to return a sequence of any RuleViolations.</span></span> <span data-ttu-id="b9086-229">以上六个规则检查只是强制执行晚餐上的字符串属性，不能为 null 或空。</span><span class="sxs-lookup"><span data-stu-id="b9086-229">The first six rule checks above simply enforce that string properties on our Dinner cannot be null or empty.</span></span> <span data-ttu-id="b9086-230">最后一个规则比较有趣，并调用 IsValidNumber （） helper 方法，我们可以将其添加到项目中，以验证 ContactPhone 数字格式是否与晚餐的国家/地区匹配。</span><span class="sxs-lookup"><span data-stu-id="b9086-230">The last rule is a little more interesting, and calls a PhoneValidator.IsValidNumber() helper method that we can add to our project to verify that the ContactPhone number format matches the Dinner's country.</span></span>

<span data-ttu-id="b9086-231">我们可以使用。为实现此电话验证支持，网络的正则表达式支持。</span><span class="sxs-lookup"><span data-stu-id="b9086-231">We can use .NET's regular expression support to implement this phone validation support.</span></span> <span data-ttu-id="b9086-232">下面是一个简单的 PhoneValidator 实现，我们可以将其添加到项目中，使我们能够添加特定于国家的 Regex 模式检查：</span><span class="sxs-lookup"><span data-stu-id="b9086-232">Below is a simple PhoneValidator implementation that we can add to our project that enables us to add country-specific Regex pattern checks:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample12.cs)]

#### <a name="handling-validation-and-business-logic-violations"></a><span data-ttu-id="b9086-233">处理验证和业务逻辑冲突</span><span class="sxs-lookup"><span data-stu-id="b9086-233">Handling Validation and Business Logic Violations</span></span>

<span data-ttu-id="b9086-234">现在，我们已添加了上述验证和业务规则代码，因此，只要我们尝试创建或更新晚餐，就会评估并强制实施验证逻辑规则。</span><span class="sxs-lookup"><span data-stu-id="b9086-234">Now that we've added the above validation and business rule code, any time we try to create or update a Dinner, our validation logic rules will be evaluated and enforced.</span></span>

<span data-ttu-id="b9086-235">开发人员可以编写如下代码来主动确定晚餐对象是否有效，并检索其中所有违规的列表而不引发任何异常：</span><span class="sxs-lookup"><span data-stu-id="b9086-235">Developers can write code like below to proactively determine if a Dinner object is valid, and retrieve a list of all violations in it without raising any exceptions:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample13.cs)]

<span data-ttu-id="b9086-236">如果尝试保存的晚餐处于无效状态，则当我们对 DinnerRepository 调用 Save （）方法时，将引发异常。</span><span class="sxs-lookup"><span data-stu-id="b9086-236">If we attempt to save a Dinner in an invalid state, an exception will be raised when we call the Save() method on the DinnerRepository.</span></span> <span data-ttu-id="b9086-237">之所以发生这种情况，是因为 LINQ to SQL 会在保存晚餐的更改之前自动调用 OnValidate （）分部方法，并且我们将代码添加到 OnValidate （）以在晚餐中存在任何规则冲突时引发异常。</span><span class="sxs-lookup"><span data-stu-id="b9086-237">This occurs because LINQ to SQL automatically calls our Dinner.OnValidate() partial method before it saves the Dinner's changes, and we added code to Dinner.OnValidate() to raise an exception if any rule violations exist in the Dinner.</span></span> <span data-ttu-id="b9086-238">我们可以捕获此异常，并被动检索要修复的冲突列表：</span><span class="sxs-lookup"><span data-stu-id="b9086-238">We can catch this exception and reactively retrieve a list of the violations to fix:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample14.cs)]

<span data-ttu-id="b9086-239">由于我们的验证和业务规则是在模型层中实现的，而不是在 UI 层内实现的，因此它们将在应用程序的所有方案中应用和使用。</span><span class="sxs-lookup"><span data-stu-id="b9086-239">Because our validation and business rules are implemented within our model layer, and not within the UI layer, they will be applied and used across all scenarios within our application.</span></span> <span data-ttu-id="b9086-240">稍后我们可以更改或添加业务规则，并让所有与晚餐对象结合使用的代码遵守这些规则。</span><span class="sxs-lookup"><span data-stu-id="b9086-240">We can later change or add business rules and have all code that works with our Dinner objects honor them.</span></span>

<span data-ttu-id="b9086-241">可以灵活地在一个位置更改业务规则，而无需在整个应用程序和 UI 逻辑中使用这些更改，这是一个编写完善的应用程序的符号，而 MVC 框架可帮助鼓励您这样做。</span><span class="sxs-lookup"><span data-stu-id="b9086-241">Having the flexibility to change business rules in one place, without having these changes ripple throughout the application and UI logic, is a sign of a well-written application, and a benefit that an MVC framework helps encourage.</span></span>

### <a name="next-step"></a><span data-ttu-id="b9086-242">下一步</span><span class="sxs-lookup"><span data-stu-id="b9086-242">Next Step</span></span>

<span data-ttu-id="b9086-243">现在，我们提供了一个可用于查询和更新数据库的模型。</span><span class="sxs-lookup"><span data-stu-id="b9086-243">We've now got a model that we can use to both query and update our database.</span></span>

<span data-ttu-id="b9086-244">现在，让我们向项目添加一些控制器和视图，我们可以使用它们来构建 HTML UI 体验。</span><span class="sxs-lookup"><span data-stu-id="b9086-244">Let's now add some controllers and views to the project that we can use to build an HTML UI experience around it.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b9086-245">[上一页](create-a-database.md)
> [下一页](use-controllers-and-views-to-implement-a-listingdetails-ui.md)</span><span class="sxs-lookup"><span data-stu-id="b9086-245">[Previous](create-a-database.md)
[Next](use-controllers-and-views-to-implement-a-listingdetails-ui.md)</span></span>
