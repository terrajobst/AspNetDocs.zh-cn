---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-2
title: 添加模型和控制器 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 88908ff8-51a9-40eb-931c-a8139128b680
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-2
msc.type: authoredcontent
ms.openlocfilehash: 57dacda421968f341284d89c9a3ad80040c16e25
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449186"
---
# <a name="add-models-and-controllers"></a><span data-ttu-id="33d23-102">添加模型和控制器</span><span class="sxs-lookup"><span data-stu-id="33d23-102">Add Models and Controllers</span></span>

<span data-ttu-id="33d23-103">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="33d23-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="33d23-104">下载完成的项目</span><span class="sxs-lookup"><span data-stu-id="33d23-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="33d23-105">在本部分中，您将添加定义数据库实体的模型类。</span><span class="sxs-lookup"><span data-stu-id="33d23-105">In this section, you will add model classes that define the database entities.</span></span> <span data-ttu-id="33d23-106">然后，将添加对这些实体执行 CRUD 操作的 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="33d23-106">Then you will add Web API controllers that perform CRUD operations on those entities.</span></span>

## <a name="add-model-classes"></a><span data-ttu-id="33d23-107">添加模型类</span><span class="sxs-lookup"><span data-stu-id="33d23-107">Add Model Classes</span></span>

<span data-ttu-id="33d23-108">在本教程中，我们将使用 "Code First" 方法实体框架（EF）创建数据库。</span><span class="sxs-lookup"><span data-stu-id="33d23-108">In this tutorial, we'll create the database by using the "Code First" approach to Entity Framework (EF).</span></span> <span data-ttu-id="33d23-109">通过 Code First，您可以C#编写与数据库表相对应的类，而 EF 会创建数据库。</span><span class="sxs-lookup"><span data-stu-id="33d23-109">With Code First, you write C# classes that correspond to database tables, and EF creates the database.</span></span> <span data-ttu-id="33d23-110">（有关详细信息，请参阅[实体框架开发方法](https://msdn.microsoft.com/library/ms178359%28v=vs.110%29.aspx#dbfmfcf)。）</span><span class="sxs-lookup"><span data-stu-id="33d23-110">(For more information, see [Entity Framework Development Approaches](https://msdn.microsoft.com/library/ms178359%28v=vs.110%29.aspx#dbfmfcf).)</span></span>

<span data-ttu-id="33d23-111">首先，我们将域对象定义为 Poco （纯旧 CLR 对象）。</span><span class="sxs-lookup"><span data-stu-id="33d23-111">We start by defining our domain objects as POCOs (plain-old CLR objects).</span></span> <span data-ttu-id="33d23-112">我们将创建以下 Poco：</span><span class="sxs-lookup"><span data-stu-id="33d23-112">We will create the following POCOs:</span></span>

- <span data-ttu-id="33d23-113">作者</span><span class="sxs-lookup"><span data-stu-id="33d23-113">Author</span></span>
- <span data-ttu-id="33d23-114">Book</span><span class="sxs-lookup"><span data-stu-id="33d23-114">Book</span></span>

<span data-ttu-id="33d23-115">在解决方案资源管理器中，右键单击 "模型" 文件夹。</span><span class="sxs-lookup"><span data-stu-id="33d23-115">In Solution Explorer, right click the Models folder.</span></span> <span data-ttu-id="33d23-116">选择 "**添加**"，然后选择 "**类**"。</span><span class="sxs-lookup"><span data-stu-id="33d23-116">Select **Add**, then select **Class**.</span></span> <span data-ttu-id="33d23-117">将此类命名为 `Author`。</span><span class="sxs-lookup"><span data-stu-id="33d23-117">Name the class `Author`.</span></span>

![](part-2/_static/image1.png)

<span data-ttu-id="33d23-118">将 Author.cs 中的所有样本代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="33d23-118">Replace all of the boilerplate code in Author.cs with the following code.</span></span>

[!code-csharp[Main](part-2/samples/sample1.cs)]

<span data-ttu-id="33d23-119">添加另一个名为 `Book`的类，其中包含以下代码。</span><span class="sxs-lookup"><span data-stu-id="33d23-119">Add another class named `Book`, with the following code.</span></span>

[!code-csharp[Main](part-2/samples/sample2.cs)]

<span data-ttu-id="33d23-120">实体框架将使用这些模型创建数据库表。</span><span class="sxs-lookup"><span data-stu-id="33d23-120">Entity Framework will use these models to create database tables.</span></span> <span data-ttu-id="33d23-121">对于每个模型，`Id` 属性将成为数据库表的主键列。</span><span class="sxs-lookup"><span data-stu-id="33d23-121">For each model, the `Id` property will become the primary key column of the database table.</span></span>

<span data-ttu-id="33d23-122">在 Book 类中，`AuthorId` 定义 `Author` 表中的外键。</span><span class="sxs-lookup"><span data-stu-id="33d23-122">In the Book class, the `AuthorId` defines a foreign key into the `Author` table.</span></span> <span data-ttu-id="33d23-123">（为简单起见，我假定每本书只有一个作者。）Book 类还包含相关 `Author`的导航属性。</span><span class="sxs-lookup"><span data-stu-id="33d23-123">(For simplicity, I'm assuming that each book has a single author.) The book class also contains a navigation property to the related `Author`.</span></span> <span data-ttu-id="33d23-124">可以使用导航属性访问代码中的相关 `Author`。</span><span class="sxs-lookup"><span data-stu-id="33d23-124">You can use the navigation property to access the related `Author` in code.</span></span> <span data-ttu-id="33d23-125">我在第4部分中详细介绍了导航属性，[处理实体关系](part-4.md)。</span><span class="sxs-lookup"><span data-stu-id="33d23-125">I say more about navigation properties in part 4, [Handling Entity Relations](part-4.md).</span></span>

## <a name="add-web-api-controllers"></a><span data-ttu-id="33d23-126">添加 Web API 控制器</span><span class="sxs-lookup"><span data-stu-id="33d23-126">Add Web API Controllers</span></span>

<span data-ttu-id="33d23-127">在本部分中，我们将添加支持 CRUD 操作（创建、读取、更新和删除）的 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="33d23-127">In this section, we'll add Web API controllers that support CRUD operations (create, read, update, and delete).</span></span> <span data-ttu-id="33d23-128">控制器将使用实体框架与数据库层进行通信。</span><span class="sxs-lookup"><span data-stu-id="33d23-128">The controllers will use Entity Framework to communicate with the database layer.</span></span>

<span data-ttu-id="33d23-129">首先，可以删除文件控制器/ValuesController。</span><span class="sxs-lookup"><span data-stu-id="33d23-129">First, you can delete the file Controllers/ValuesController.cs.</span></span> <span data-ttu-id="33d23-130">此文件包含一个示例 Web API 控制器，但本教程不需要此文件。</span><span class="sxs-lookup"><span data-stu-id="33d23-130">This file contains an example Web API controller, but you don't need it for this tutorial.</span></span>

![](part-2/_static/image2.png)

<span data-ttu-id="33d23-131">接下来，生成项目。</span><span class="sxs-lookup"><span data-stu-id="33d23-131">Next, build the project.</span></span> <span data-ttu-id="33d23-132">Web API 基架使用反射查找模型类，因此它需要编译的程序集。</span><span class="sxs-lookup"><span data-stu-id="33d23-132">The Web API scaffolding uses reflection to find the model classes, so it needs the compiled assembly.</span></span>

<span data-ttu-id="33d23-133">在解决方案资源管理器中，右键单击 "控制器" 文件夹。</span><span class="sxs-lookup"><span data-stu-id="33d23-133">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="33d23-134">选择 "**添加**"，然后选择 "**控制器**"。</span><span class="sxs-lookup"><span data-stu-id="33d23-134">Select **Add**, then select **Controller**.</span></span>

![](part-2/_static/image3.png)

<span data-ttu-id="33d23-135">在 "**添加基架**" 对话框中，选择 "包含操作的 Web API 2 控制器，使用实体框架"。</span><span class="sxs-lookup"><span data-stu-id="33d23-135">In the **Add Scaffold** dialog, select "Web API 2 Controller with actions, using Entity Framework".</span></span> <span data-ttu-id="33d23-136">单击 **“添加”** 。</span><span class="sxs-lookup"><span data-stu-id="33d23-136">Click **Add**.</span></span>

![](part-2/_static/image4.png)

<span data-ttu-id="33d23-137">在 "**添加控制器**" 对话框中，执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="33d23-137">In the **Add Controller** dialog, do the following:</span></span>

1. <span data-ttu-id="33d23-138">在 "**模型类**" 下拉列表中，选择 `Author` 类。</span><span class="sxs-lookup"><span data-stu-id="33d23-138">In the **Model class** dropdown, select the `Author` class.</span></span> <span data-ttu-id="33d23-139">（如果未在下拉列表中看到它，请确保生成了项目。）</span><span class="sxs-lookup"><span data-stu-id="33d23-139">(If you don't see it listed in the dropdown, make sure that you built the project.)</span></span>
2. <span data-ttu-id="33d23-140">选中 "使用异步控制器操作"。</span><span class="sxs-lookup"><span data-stu-id="33d23-140">Check "Use async controller actions".</span></span>
3. <span data-ttu-id="33d23-141">将控制器名称保留为 &quot;AuthorsController&quot;。</span><span class="sxs-lookup"><span data-stu-id="33d23-141">Leave the controller name as &quot;AuthorsController&quot;.</span></span>
4. <span data-ttu-id="33d23-142">单击 "**数据上下文类**" 旁边的加号（+）按钮。</span><span class="sxs-lookup"><span data-stu-id="33d23-142">Click plus (+) button next to **Data Context Class**.</span></span>

![](part-2/_static/image5.png)

<span data-ttu-id="33d23-143">在 "**新建数据上下文**" 对话框中，保留默认名称，然后单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="33d23-143">In the **New Data Context** dialog, leave the default name and click **Add**.</span></span>

![](part-2/_static/image6.png)

<span data-ttu-id="33d23-144">单击 "**添加**" 以完成 "**添加控制器**" 对话框。</span><span class="sxs-lookup"><span data-stu-id="33d23-144">Click **Add** to complete the **Add Controller** dialog.</span></span> <span data-ttu-id="33d23-145">此对话框将两个类添加到项目中：</span><span class="sxs-lookup"><span data-stu-id="33d23-145">The dialog adds two classes to your project:</span></span>

- <span data-ttu-id="33d23-146">`AuthorsController` 定义 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="33d23-146">`AuthorsController` defines a Web API controller.</span></span> <span data-ttu-id="33d23-147">控制器实现了客户端用于对作者列表执行 CRUD 操作的 REST API。</span><span class="sxs-lookup"><span data-stu-id="33d23-147">The controller implements the REST API that clients use to perform CRUD operations on the list of authors.</span></span>
- <span data-ttu-id="33d23-148">`BookServiceContext` 在运行时管理实体对象，这包括使用数据库中的数据填充对象、更改跟踪以及将数据保存到数据库。</span><span class="sxs-lookup"><span data-stu-id="33d23-148">`BookServiceContext` manages entity objects during run time, which includes populating objects with data from a database, change tracking, and persisting data to the database.</span></span> <span data-ttu-id="33d23-149">它继承自 `DbContext`。</span><span class="sxs-lookup"><span data-stu-id="33d23-149">It inherits from `DbContext`.</span></span>

![](part-2/_static/image7.png)

<span data-ttu-id="33d23-150">此时，请重新生成项目。</span><span class="sxs-lookup"><span data-stu-id="33d23-150">At this point, build the project again.</span></span> <span data-ttu-id="33d23-151">现在，请执行相同的步骤，为 `Book` 实体添加 API 控制器。</span><span class="sxs-lookup"><span data-stu-id="33d23-151">Now go through the same steps to add an API controller for `Book` entities.</span></span> <span data-ttu-id="33d23-152">这一次，请选择模型类 `Book`，并为数据上下文类选择现有 `BookServiceContext` 类。</span><span class="sxs-lookup"><span data-stu-id="33d23-152">This time, select `Book` for the model class, and select the existing `BookServiceContext` class for the data context class.</span></span> <span data-ttu-id="33d23-153">（请勿创建新的数据上下文。）单击 "**添加**" 以添加该控制器。</span><span class="sxs-lookup"><span data-stu-id="33d23-153">(Don't create a new data context.) Click **Add** to add the controller.</span></span>

![](part-2/_static/image8.png)

> [!div class="step-by-step"]
> <span data-ttu-id="33d23-154">[上一页](part-1.md)
> [下一页](part-3.md)</span><span class="sxs-lookup"><span data-stu-id="33d23-154">[Previous](part-1.md)
[Next](part-3.md)</span></span>
