---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-cs
title: 用实体框架（C#）创建模型类 |Microsoft Docs
author: microsoft
description: 在本教程中，了解如何将 ASP.NET MVC 与 Microsoft 实体框架结合使用。 了解如何使用实体向导创建 ADO.NET 实体 Da 。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 61644169-e8b1-45dd-bf96-9c2301b69879
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-cs
msc.type: authoredcontent
ms.openlocfilehash: 2e0e365c287fc455015d237ea466301335805d14
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78469436"
---
# <a name="creating-model-classes-with-the-entity-framework-c"></a><span data-ttu-id="9f5f9-104">使用 Entity Framework 创建模型类 (C#)</span><span class="sxs-lookup"><span data-stu-id="9f5f9-104">Creating Model Classes with the Entity Framework (C#)</span></span>

<span data-ttu-id="9f5f9-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="9f5f9-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="9f5f9-106">在本教程中，了解如何将 ASP.NET MVC 与 Microsoft 实体框架结合使用。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-106">In this tutorial, you learn how to use ASP.NET MVC with the Microsoft Entity Framework.</span></span> <span data-ttu-id="9f5f9-107">了解如何使用实体向导创建 ADO.NET 实体数据模型。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-107">You learn how to use the Entity Wizard to create an ADO.NET Entity Data Model.</span></span> <span data-ttu-id="9f5f9-108">在本教程中，我们将构建一个 web 应用程序，该应用程序演示如何使用实体框架来选择、插入、更新和删除数据库数据。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-108">Over the course of this tutorial, we build a web application that illustrates how to select, insert, update, and delete database data by using the Entity Framework.</span></span>

<span data-ttu-id="9f5f9-109">本教程的目的是说明如何在生成 ASP.NET MVC 应用程序时使用 Microsoft 实体框架来创建数据访问类。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-109">The goal of this tutorial is to explain how you can create data access classes using the Microsoft Entity Framework when building an ASP.NET MVC application.</span></span> <span data-ttu-id="9f5f9-110">本教程假定你以前没有 Microsoft 实体框架知识。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-110">This tutorial assumes no previous knowledge of the Microsoft Entity Framework.</span></span> <span data-ttu-id="9f5f9-111">在本教程结束时，您将了解如何使用实体框架来选择、插入、更新和删除数据库记录。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-111">By the end of this tutorial, you'll understand how to use the Entity Framework to select, insert, update, and delete database records.</span></span>

<span data-ttu-id="9f5f9-112">Microsoft 实体框架是一种对象关系映射（O/RM）工具，它使您能够从数据库中自动生成数据访问层。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-112">The Microsoft Entity Framework is an Object Relational Mapping (O/RM) tool that enables you to generate a data access layer from a database automatically.</span></span> <span data-ttu-id="9f5f9-113">使用实体框架可以避免手动生成数据访问类的单调工作。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-113">The Entity Framework enables you to avoid the tedious work of building your data access classes by hand.</span></span>

<span data-ttu-id="9f5f9-114">为了说明如何将 Microsoft 实体框架与 ASP.NET MVC 结合使用，我们将构建一个简单的示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-114">In order to illustrate how you can use the Microsoft Entity Framework with ASP.NET MVC, we'll build a simple sample application.</span></span> <span data-ttu-id="9f5f9-115">我们将创建一个电影数据库应用程序，用于显示和编辑电影数据库记录。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-115">We'll create a Movie Database application that enables you to display and edit movie database records.</span></span>

<span data-ttu-id="9f5f9-116">本教程假定你具有 Visual Studio 2008 或带有 Service Pack 1 的 Visual Web Developer 2008。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-116">This tutorial assumes that you have Visual Studio 2008 or Visual Web Developer 2008 with Service Pack 1.</span></span> <span data-ttu-id="9f5f9-117">需要 Service Pack 1 才能使用实体框架。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-117">You need Service Pack 1 in order to use the Entity Framework.</span></span> <span data-ttu-id="9f5f9-118">你可以从以下地址下载 Visual Studio 2008 Service Pack 1 或带 Service Pack 1 的 Visual Web Developer：</span><span class="sxs-lookup"><span data-stu-id="9f5f9-118">You can download Visual Studio 2008 Service Pack 1 or Visual Web Developer with Service Pack 1 from the following address:</span></span>

> [https://www.asp.net/downloads/](https://www.asp.net/downloads)

> [!NOTE] 
> 
> <span data-ttu-id="9f5f9-119">ASP.NET MVC 与 Microsoft 实体框架之间没有必要的连接。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-119">There is no essential connection between ASP.NET MVC and the Microsoft Entity Framework.</span></span> <span data-ttu-id="9f5f9-120">可以将实体框架一些替代方法用于 ASP.NET MVC。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-120">There are several alternatives to the Entity Framework that you can use with ASP.NET MVC.</span></span> <span data-ttu-id="9f5f9-121">例如，你可以使用其他 O/RM 工具（如 Microsoft LINQ to SQL、NHibernate 或 SubSonic）来构建 MVC 模型类。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-121">For example, you can build your MVC Model classes using other O/RM tools such as Microsoft LINQ to SQL, NHibernate, or SubSonic.</span></span>

## <a name="creating-the-movie-sample-database"></a><span data-ttu-id="9f5f9-122">创建电影示例数据库</span><span class="sxs-lookup"><span data-stu-id="9f5f9-122">Creating the Movie Sample Database</span></span>

<span data-ttu-id="9f5f9-123">电影数据库应用程序使用名为电影的数据库表，其中包含以下列：</span><span class="sxs-lookup"><span data-stu-id="9f5f9-123">The Movie Database application uses a database table named Movies that contains the following columns:</span></span>

| <span data-ttu-id="9f5f9-124">列名</span><span class="sxs-lookup"><span data-stu-id="9f5f9-124">Column Name</span></span> | <span data-ttu-id="9f5f9-125">数据类型</span><span class="sxs-lookup"><span data-stu-id="9f5f9-125">Data Type</span></span> | <span data-ttu-id="9f5f9-126">是否允许空？</span><span class="sxs-lookup"><span data-stu-id="9f5f9-126">Allow Nulls?</span></span> | <span data-ttu-id="9f5f9-127">为主键？</span><span class="sxs-lookup"><span data-stu-id="9f5f9-127">Is Primary Key?</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9f5f9-128">Id</span><span class="sxs-lookup"><span data-stu-id="9f5f9-128">Id</span></span> | <span data-ttu-id="9f5f9-129">int</span><span class="sxs-lookup"><span data-stu-id="9f5f9-129">int</span></span> | <span data-ttu-id="9f5f9-130">False</span><span class="sxs-lookup"><span data-stu-id="9f5f9-130">False</span></span> | <span data-ttu-id="9f5f9-131">True</span><span class="sxs-lookup"><span data-stu-id="9f5f9-131">True</span></span> |
| <span data-ttu-id="9f5f9-132">标题</span><span class="sxs-lookup"><span data-stu-id="9f5f9-132">Title</span></span> | <span data-ttu-id="9f5f9-133">nvarchar(100)</span><span class="sxs-lookup"><span data-stu-id="9f5f9-133">nvarchar(100)</span></span> | <span data-ttu-id="9f5f9-134">False</span><span class="sxs-lookup"><span data-stu-id="9f5f9-134">False</span></span> | <span data-ttu-id="9f5f9-135">False</span><span class="sxs-lookup"><span data-stu-id="9f5f9-135">False</span></span> |
| <span data-ttu-id="9f5f9-136">导演</span><span class="sxs-lookup"><span data-stu-id="9f5f9-136">Director</span></span> | <span data-ttu-id="9f5f9-137">nvarchar(100)</span><span class="sxs-lookup"><span data-stu-id="9f5f9-137">nvarchar(100)</span></span> | <span data-ttu-id="9f5f9-138">False</span><span class="sxs-lookup"><span data-stu-id="9f5f9-138">False</span></span> | <span data-ttu-id="9f5f9-139">False</span><span class="sxs-lookup"><span data-stu-id="9f5f9-139">False</span></span> |

<span data-ttu-id="9f5f9-140">可以通过以下步骤将此表添加到 ASP.NET MVC 项目：</span><span class="sxs-lookup"><span data-stu-id="9f5f9-140">You can add this table to an ASP.NET MVC project by following these steps:</span></span>

1. <span data-ttu-id="9f5f9-141">右键单击 "解决方案资源管理器" 窗口中的 "应用\_Data" 文件夹，然后选择 "**添加"、"新建项**" 菜单。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-141">Right-click the App\_Data folder in the Solution Explorer window and select the menu option **Add, New Item.**</span></span>
2. <span data-ttu-id="9f5f9-142">从 "**添加新项**" 对话框中，选择 " **SQL Server 数据库**"，为数据库指定名称 MoviesDB，然后单击 "**添加**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-142">From the **Add New Item** dialog box, select **SQL Server Database**, give the database the name MoviesDB.mdf, and click the **Add** button.</span></span>
3. <span data-ttu-id="9f5f9-143">双击 MoviesDB 文件以打开 "服务器资源管理器/数据库资源管理器" 窗口。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-143">Double-click the MoviesDB.mdf file to open the Server Explorer/Database Explorer window.</span></span>
4. <span data-ttu-id="9f5f9-144">展开 "MoviesDB" 数据库连接，右键单击 "表" 文件夹，然后选择 "**添加新表**" 菜单选项。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-144">Expand the MoviesDB.mdf database connection, right-click the Tables folder, and select the menu option **Add New Table**.</span></span>
5. <span data-ttu-id="9f5f9-145">在表设计器中，添加 "Id"、"标题" 和 "主管" 列。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-145">In the Table Designer, add the Id, Title, and Director columns.</span></span>
6. <span data-ttu-id="9f5f9-146">单击 "**保存**" 按钮（它具有软盘图标），以将新表保存为电影名称。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-146">Click the **Save** button (it has the icon of the floppy) to save the new table with the name Movies.</span></span>

<span data-ttu-id="9f5f9-147">创建电影数据库表后，应将一些示例数据添加到表中。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-147">After you create the Movies database table, you should add some sample data to the table.</span></span> <span data-ttu-id="9f5f9-148">右键单击电影表，然后选择菜单选项 "**显示表数据**"。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-148">Right-click the Movies table and select the menu option **Show Table Data**.</span></span> <span data-ttu-id="9f5f9-149">可以在显示的网格中输入虚假电影数据。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-149">You can enter fake movie data into the grid that appears.</span></span>

## <a name="creating-the-adonet-entity-data-model"></a><span data-ttu-id="9f5f9-150">创建 ADO.NET 实体数据模型</span><span class="sxs-lookup"><span data-stu-id="9f5f9-150">Creating the ADO.NET Entity Data Model</span></span>

<span data-ttu-id="9f5f9-151">若要使用实体框架，需要创建一个实体数据模型。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-151">In order to use the Entity Framework, you need to create an Entity Data Model.</span></span> <span data-ttu-id="9f5f9-152">你可以利用 Visual Studio*实体数据模型向导*来自动从数据库生成实体数据模型。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-152">You can take advantage of the Visual Studio *Entity Data Model Wizard* to generate an Entity Data Model from a database automatically.</span></span>

<span data-ttu-id="9f5f9-153">请执行这些步骤：</span><span class="sxs-lookup"><span data-stu-id="9f5f9-153">Follow these steps:</span></span>

1. <span data-ttu-id="9f5f9-154">右键单击 "解决方案资源管理器" 窗口中的 "模型" 文件夹，然后选择 "**添加"、"新建项**" 菜单。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-154">Right-click the Models folder in the Solution Explorer window and select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="9f5f9-155">在 "**添加新项**" 对话框中，选择数据类别（请参阅图1）。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-155">In the **Add New Item** dialog, select the Data category (see Figure 1).</span></span>
3. <span data-ttu-id="9f5f9-156">选择 " **ADO.NET 实体数据模型**" 模板，将 "名称" 指定实体数据模型为 "MoviesDBModel"，然后单击 "**添加**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-156">Select the **ADO.NET Entity Data Model** template, give the Entity Data Model the name MoviesDBModel.edmx, and click the **Add** button.</span></span> <span data-ttu-id="9f5f9-157">单击 "**添加**" 按钮将启动数据模型向导。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-157">Clicking the **Add** button launches the Data Model Wizard.</span></span>
4. <span data-ttu-id="9f5f9-158">在 "**选择模型内容**" 步骤中，选择 "**从数据库生成**" 选项，然后单击 "**下一步**" 按钮（参见图2）。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-158">In the **Choose Model Contents** step, choose the **Generate from a database** option and click the **Next** button (see Figure 2).</span></span>
5. <span data-ttu-id="9f5f9-159">在 "**选择你的数据连接**" 步骤中，选择 "MoviesDB" 数据库连接，输入实体连接设置 "名称 MoviesDBEntities"，然后单击 "**下一步**" 按钮（见图3）。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-159">In the **Choose Your Data Connection** step, select the MoviesDB.mdf database connection, enter the entities connection settings name MoviesDBEntities, and click the **Next** button (see Figure 3).</span></span>
6. <span data-ttu-id="9f5f9-160">在 "**选择数据库对象**" 步骤中，选择 "电影数据库" 表，然后单击 "**完成**" 按钮（见图4）。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-160">In the **Choose Your Database Objects** step, select the Movie database table and click the **Finish** button (see Figure 4).</span></span>

<span data-ttu-id="9f5f9-161">完成这些步骤后，将打开 "ADO.NET 实体数据模型设计器（Entity Designer）"。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-161">After you complete these steps, the ADO.NET Entity Data Model Designer (Entity Designer) opens.</span></span>

<span data-ttu-id="9f5f9-162">**图 1-创建新实体数据模型**</span><span class="sxs-lookup"><span data-stu-id="9f5f9-162">**Figure 1 – Creating a new Entity Data Model**</span></span>

![clip_image002](creating-model-classes-with-the-entity-framework-cs/_static/image1.jpg)

<span data-ttu-id="9f5f9-164">**图 2-选择模型内容步骤**</span><span class="sxs-lookup"><span data-stu-id="9f5f9-164">**Figure 2 – Choose Model Contents Step**</span></span>

![clip_image004](creating-model-classes-with-the-entity-framework-cs/_static/image2.jpg)

<span data-ttu-id="9f5f9-166">**图 3-选择你的数据连接**</span><span class="sxs-lookup"><span data-stu-id="9f5f9-166">**Figure 3 – Choose Your Data Connection**</span></span>

![clip_image006](creating-model-classes-with-the-entity-framework-cs/_static/image3.jpg)

<span data-ttu-id="9f5f9-168">**图 4-选择数据库对象**</span><span class="sxs-lookup"><span data-stu-id="9f5f9-168">**Figure 4 – Choose Your Database Objects**</span></span>

![clip_image008](creating-model-classes-with-the-entity-framework-cs/_static/image4.jpg)

#### <a name="modifying-the-adonet-entity-data-model"></a><span data-ttu-id="9f5f9-170">修改 ADO.NET 实体数据模型</span><span class="sxs-lookup"><span data-stu-id="9f5f9-170">Modifying the ADO.NET Entity Data Model</span></span>

<span data-ttu-id="9f5f9-171">创建实体数据模型后，可以通过利用 Entity Designer 来修改模型（请参阅图5）。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-171">After you create an Entity Data Model, you can modify the model by taking advantage of the Entity Designer (see Figure 5).</span></span> <span data-ttu-id="9f5f9-172">您可以通过双击 "解决方案资源管理器" 窗口中的 "模型" 文件夹中包含的 "MoviesDBModel" 文件，随时打开 Entity Designer。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-172">You can open the Entity Designer at any time by double-clicking the MoviesDBModel.edmx file contained in the Models folder within the Solution Explorer window.</span></span>

<span data-ttu-id="9f5f9-173">**图5– ADO.NET 实体数据模型设计器**</span><span class="sxs-lookup"><span data-stu-id="9f5f9-173">**Figure 5 – The ADO.NET Entity Data Model Designer**</span></span>

![clip_image010](creating-model-classes-with-the-entity-framework-cs/_static/image5.jpg)

<span data-ttu-id="9f5f9-175">例如，您可以使用 Entity Designer 更改实体模型数据向导生成的类的名称。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-175">For example, you can use the Entity Designer to change the names of the classes that the Entity Model Data Wizard generates.</span></span> <span data-ttu-id="9f5f9-176">向导已创建名为 "电影" 的新数据访问类。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-176">The Wizard created a new data access class named Movies.</span></span> <span data-ttu-id="9f5f9-177">换言之，向导为类提供与数据库表的名称相同的名称。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-177">In other words, the Wizard gave the class the very same name as the database table.</span></span> <span data-ttu-id="9f5f9-178">由于我们将使用此类来表示特定的电影实例，因此应将类从电影重命名为电影。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-178">Because we will use this class to represent a particular Movie instance, we should rename the class from Movies to Movie.</span></span>

<span data-ttu-id="9f5f9-179">如果要重命名实体类，可以双击 "Entity Designer 中的类名称，然后输入新名称（见图6）。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-179">If you want to rename an entity class, you can double-click on the class name in the Entity Designer and enter a new name (see Figure 6).</span></span> <span data-ttu-id="9f5f9-180">或者，在 Entity Designer 中选择实体后，可以更改属性窗口中的实体的名称。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-180">Alternatively, you can change the name of an entity in the Properties window after selecting an entity in the Entity Designer.</span></span>

<span data-ttu-id="9f5f9-181">**图 6-更改实体名称**</span><span class="sxs-lookup"><span data-stu-id="9f5f9-181">**Figure 6 – Changing an entity name**</span></span>

![clip_image012](creating-model-classes-with-the-entity-framework-cs/_static/image6.jpg)

<span data-ttu-id="9f5f9-183">请记住在进行修改后保存实体数据模型，方法是单击 "保存" 按钮（软盘的图标）。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-183">Remember to save your Entity Data Model after making a modification by clicking the Save button (the icon of the floppy disk).</span></span> <span data-ttu-id="9f5f9-184">在幕后，Entity Designer 将生成一组C#类。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-184">Behind the scenes, the Entity Designer generates a set of C# classes.</span></span> <span data-ttu-id="9f5f9-185">您可以通过从 "解决方案资源管理器" 窗口打开 MoviesDBModel.Designer.cs 文件来查看这些类。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-185">You can view these classes by opening the MoviesDBModel.Designer.cs file from the Solution Explorer window.</span></span>

<span data-ttu-id="9f5f9-186">请勿修改 Designer.cs 文件中的代码，因为下次使用 Entity Designer 时，所做的更改将被覆盖。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-186">Don't modify the code in the Designer.cs file since your changes will be overwritten the next time you use the Entity Designer.</span></span> <span data-ttu-id="9f5f9-187">如果要扩展 Designer.cs 文件中定义的实体类的功能，则可以在单独的文件中创建*分部类*。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-187">If you want to extend the functionality of the entity classes defined in the Designer.cs file then you can create *partial classes* in separate files.</span></span>

#### <a name="selecting-database-records-with-the-entity-framework"></a><span data-ttu-id="9f5f9-188">选择包含实体框架的数据库记录</span><span class="sxs-lookup"><span data-stu-id="9f5f9-188">Selecting Database Records with the Entity Framework</span></span>

<span data-ttu-id="9f5f9-189">接下来，我们将创建一个显示电影记录列表的页面，开始构建电影数据库应用程序。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-189">Let's start building our Movie Database application by creating a page that displays a list of movie records.</span></span> <span data-ttu-id="9f5f9-190">列表1中的 Home 控制器公开一个名为 Index （）的操作。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-190">The Home controller in Listing 1 exposes an action named Index().</span></span> <span data-ttu-id="9f5f9-191">Index （）操作利用实体框架从电影数据库表中返回所有电影记录。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-191">The Index() action returns all of the movie records from the Movie database table by taking advantage of the Entity Framework.</span></span>

<span data-ttu-id="9f5f9-192">**列表1– Controllers\HomeController.cs**</span><span class="sxs-lookup"><span data-stu-id="9f5f9-192">**Listing 1 – Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample1.cs)]

<span data-ttu-id="9f5f9-193">请注意，列表1中的控制器包含构造函数。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-193">Notice that the controller in Listing 1 includes a constructor.</span></span> <span data-ttu-id="9f5f9-194">构造函数初始化名为 \_db 的类级字段。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-194">The constructor initializes a class-level field named \_db.</span></span> <span data-ttu-id="9f5f9-195">\_db 字段表示由 Microsoft 实体框架生成的数据库实体。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-195">The \_db field represents the database entities generated by the Microsoft Entity Framework.</span></span> <span data-ttu-id="9f5f9-196">\_db 字段是 Entity Designer 生成的 MoviesDBEntities 类的实例。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-196">The \_db field is an instance of the MoviesDBEntities class that was generated by the Entity Designer.</span></span>

<span data-ttu-id="9f5f9-197">若要在 Home 控制器中使用 theMoviesDBEntities 类，必须导入 MovieEntityApp 命名空间（*MVCProjectName*）。型号）。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-197">In order to use theMoviesDBEntities class in the Home controller, you must import the MovieEntityApp.Models namespace (*MVCProjectName*.Models).</span></span>

<span data-ttu-id="9f5f9-198">\_db 字段用于索引（）操作，用于从电影数据库表中检索记录。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-198">The \_db field is used within the Index() action to retrieve the records from the Movies database table.</span></span> <span data-ttu-id="9f5f9-199">表达式 \_db。MovieSet 表示电影数据库表中的所有记录。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-199">The expression \_db.MovieSet represents all of the records from the Movies database table.</span></span> <span data-ttu-id="9f5f9-200">System.linq.enumerable.tolist （）方法用于将电影集转换为电影对象的泛型集合（List&lt;Movie&gt;）。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-200">The ToList() method is used to convert the set of movies into a generic collection of Movie objects (List&lt;Movie&gt;).</span></span>

<span data-ttu-id="9f5f9-201">可以通过 LINQ to Entities 的帮助检索电影记录。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-201">The movie records are retrieved with the help of LINQ to Entities.</span></span> <span data-ttu-id="9f5f9-202">列表1中的 Index （）操作使用 LINQ*方法语法*来检索数据库记录集。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-202">The Index() action in Listing 1 uses LINQ *method syntax* to retrieve the set of database records.</span></span> <span data-ttu-id="9f5f9-203">如果您愿意，也可以改用 LINQ*查询语法*。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-203">If you prefer, you can use LINQ *query syntax* instead.</span></span> <span data-ttu-id="9f5f9-204">以下两个语句执行的操作完全相同：</span><span class="sxs-lookup"><span data-stu-id="9f5f9-204">The following two statements do the very same thing:</span></span>

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample2.cs)]

<span data-ttu-id="9f5f9-205">使用您最直观的任何 LINQ 语法–方法语法或查询语法。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-205">Use whichever LINQ syntax – method syntax or query syntax – that you find most intuitive.</span></span> <span data-ttu-id="9f5f9-206">这两种方法之间没有性能差异–唯一的区别在于样式。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-206">There is no difference in performance between the two approaches – the only difference is style.</span></span>

<span data-ttu-id="9f5f9-207">清单2中的视图用于显示电影记录。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-207">The view in Listing 2 is used to display the movie records.</span></span>

<span data-ttu-id="9f5f9-208">**列表 2-Views\Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="9f5f9-208">**Listing 2 – Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample3.aspx)]

<span data-ttu-id="9f5f9-209">清单2中的视图包含一个**foreach**循环，该循环可循环访问每个电影记录，并显示电影记录的 "标题" 和 "控制器" 属性的值。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-209">The view in Listing 2 contains a **foreach** loop that iterates through each movie record and displays the values of the movie record's Title and Director properties.</span></span> <span data-ttu-id="9f5f9-210">请注意，"编辑" 和 "删除" 链接将显示在每个记录的旁边。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-210">Notice that an Edit and Delete link is displayed next to each record.</span></span> <span data-ttu-id="9f5f9-211">此外，"添加电影" 链接将显示在视图的底部（请参阅图7）。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-211">Furthermore, an Add Movie link appears at the bottom of the view (see Figure 7).</span></span>

<span data-ttu-id="9f5f9-212">**图7–索引视图**</span><span class="sxs-lookup"><span data-stu-id="9f5f9-212">**Figure 7 – The Index view**</span></span>

![clip_image014](creating-model-classes-with-the-entity-framework-cs/_static/image7.jpg)

<span data-ttu-id="9f5f9-214">索引视图是*类型化的视图*。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-214">The Index view is a *typed view*.</span></span> <span data-ttu-id="9f5f9-215">索引视图包含一个 &lt;% @ Page%&gt; 指令，其中包含一个*Inherits*属性，该属性将模型属性强制转换为电影对象的强类型化的泛型列表集合（List&lt;电影）。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-215">The Index view includes a &lt;%@ Page %&gt; directive with an *Inherits* attribute that casts the Model property to a strongly typed generic List collection of Movie objects (List&lt;Movie).</span></span>

## <a name="inserting-database-records-with-the-entity-framework"></a><span data-ttu-id="9f5f9-216">插入具有实体框架的数据库记录</span><span class="sxs-lookup"><span data-stu-id="9f5f9-216">Inserting Database Records with the Entity Framework</span></span>

<span data-ttu-id="9f5f9-217">您可以使用实体框架以便于将新记录插入数据库表中。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-217">You can use the Entity Framework to make it easy to insert new records into a database table.</span></span> <span data-ttu-id="9f5f9-218">列表3包含向 Home 控制器类添加的两个新操作，可用于将新记录插入到电影数据库表中。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-218">Listing 3 contains two new actions added to the Home controller class that you can use to insert new records into the Movie database table.</span></span>

<span data-ttu-id="9f5f9-219">**列表3– Controllers\HomeController.cs （添加方法）**</span><span class="sxs-lookup"><span data-stu-id="9f5f9-219">**Listing 3 – Controllers\HomeController.cs (Add methods)**</span></span>

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample4.cs)]

<span data-ttu-id="9f5f9-220">第一个 Add （）操作只返回视图。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-220">The first Add() action simply returns a view.</span></span> <span data-ttu-id="9f5f9-221">视图包含用于添加新的电影数据库记录的窗体（参见图8）。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-221">The view contains a form for adding a new movie database record (see Figure 8).</span></span> <span data-ttu-id="9f5f9-222">提交窗体时，将调用第二个 Add （）操作。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-222">When you submit the form, the second Add() action is invoked.</span></span>

<span data-ttu-id="9f5f9-223">请注意，第二个 Add （）操作是用 AcceptVerbs 特性修饰的。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-223">Notice that the second Add() action is decorated with the AcceptVerbs attribute.</span></span> <span data-ttu-id="9f5f9-224">此操作只能在执行 HTTP POST 操作时调用。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-224">This action can be invoked only when performing an HTTP POST operation.</span></span> <span data-ttu-id="9f5f9-225">换句话说，此操作只能在发布 HTML 窗体时调用。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-225">In other words, this action can only be invoked when posting an HTML form.</span></span>

<span data-ttu-id="9f5f9-226">第二个 Add （）操作使用 ASP.NET MVC TryUpdateModel （）方法的帮助创建实体框架 Movie 类的新实例。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-226">The second Add() action creates a new instance of the Entity Framework Movie class with the help of the ASP.NET MVC TryUpdateModel() method.</span></span> <span data-ttu-id="9f5f9-227">TryUpdateModel （）方法使用传递给 Add （）方法的 FormCollection 中的字段，并将这些 HTML 窗体字段的值分配给 Movie 类。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-227">The TryUpdateModel() method takes the fields in the FormCollection passed to the Add() method and assigns the values of these HTML form fields to the Movie class.</span></span>

<span data-ttu-id="9f5f9-228">使用实体框架时，在使用 TryUpdateModel 或 UpdateModel 方法更新实体类的属性时，必须提供属性的 "白列表"。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-228">When using the Entity Framework, you must supply a "white list" of properties when using the TryUpdateModel or UpdateModel methods to update the properties of an entity class.</span></span>

<span data-ttu-id="9f5f9-229">接下来，Add （）操作执行一些简单的窗体验证。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-229">Next, the Add() action performs some simple form validation.</span></span> <span data-ttu-id="9f5f9-230">操作将验证 Title 和 Director 属性是否都具有值。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-230">The action verifies that both the Title and Director properties have values.</span></span> <span data-ttu-id="9f5f9-231">如果存在验证错误，则会将验证错误消息添加到 ModelState。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-231">If there is a validation error, then a validation error message is added to ModelState.</span></span>

<span data-ttu-id="9f5f9-232">如果没有验证错误，则会将一个新的电影记录添加到 "电影数据库" 表，并提供实体框架的帮助。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-232">If there are no validation errors then a new movie record is added to the Movies database table with the help of the Entity Framework.</span></span> <span data-ttu-id="9f5f9-233">新记录将添加到数据库，其中包含以下两行代码：</span><span class="sxs-lookup"><span data-stu-id="9f5f9-233">The new record is added to the database with the following two lines of code:</span></span>

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample5.cs)]

<span data-ttu-id="9f5f9-234">第一行代码将新的 Movie 实体添加到实体框架正在跟踪的电影集。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-234">The first line of code adds the new Movie entity to the set of movies being tracked by the Entity Framework.</span></span> <span data-ttu-id="9f5f9-235">第二行代码保存对要追溯到基础数据库的电影所做的任何更改。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-235">The second line of code saves whatever changes have been made to the Movies being tracked back to the underlying database.</span></span>

<span data-ttu-id="9f5f9-236">**图8– "添加" 视图**</span><span class="sxs-lookup"><span data-stu-id="9f5f9-236">**Figure 8 – The Add view**</span></span>

![clip_image016](creating-model-classes-with-the-entity-framework-cs/_static/image8.jpg)

#### <a name="updating-database-records-with-the-entity-framework"></a><span data-ttu-id="9f5f9-238">用实体框架更新数据库记录</span><span class="sxs-lookup"><span data-stu-id="9f5f9-238">Updating Database Records with the Entity Framework</span></span>

<span data-ttu-id="9f5f9-239">您可以遵循与使用实体框架相同的方法编辑数据库记录，就像我们在插入新的数据库记录的方法一样。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-239">You can follow almost the same approach to edit a database record with the Entity Framework as the approach that we just followed to insert a new database record.</span></span> <span data-ttu-id="9f5f9-240">列表4包含两个名为 Edit （）的新控制器操作。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-240">Listing 4 contains two new controller actions named Edit().</span></span> <span data-ttu-id="9f5f9-241">第一个 Edit （）操作返回用于编辑电影记录的 HTML 窗体。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-241">The first Edit() action returns an HTML form for editing a movie record.</span></span> <span data-ttu-id="9f5f9-242">第二个 Edit （）操作尝试更新数据库。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-242">The second Edit() action attempts to update the database.</span></span>

<span data-ttu-id="9f5f9-243">**列表4– Controllers\HomeController.cs （编辑方法）**</span><span class="sxs-lookup"><span data-stu-id="9f5f9-243">**Listing 4 – Controllers\HomeController.cs (Edit methods)**</span></span>

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample6.cs)]

<span data-ttu-id="9f5f9-244">第二个 Edit （）操作通过从数据库检索与正在编辑的电影的 Id 相匹配的电影记录开始。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-244">The second Edit() action starts by retrieving the Movie record from the database that matches the Id of the movie being edited.</span></span> <span data-ttu-id="9f5f9-245">下面的 LINQ to Entities 语句获取与特定 Id 匹配的第一个数据库记录：</span><span class="sxs-lookup"><span data-stu-id="9f5f9-245">The following LINQ to Entities statement grabs the first database record that matches a particular Id:</span></span>

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample7.cs)]

<span data-ttu-id="9f5f9-246">接下来，使用 TryUpdateModel （）方法将 HTML 窗体字段的值分配给 movie 实体的属性。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-246">Next, the TryUpdateModel() method is used to assign the values of the HTML form fields to the properties of the movie entity.</span></span> <span data-ttu-id="9f5f9-247">请注意，提供允许列表来指定要更新的确切属性。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-247">Notice that a white list is supplied to specify the exact properties to update.</span></span>

<span data-ttu-id="9f5f9-248">接下来，执行一些简单的验证来验证电影标题和控制器属性是否都具有值。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-248">Next, some simple validation is performed to verify that both the Movie Title and Director properties have values.</span></span> <span data-ttu-id="9f5f9-249">如果任一属性缺少值，则会将验证错误消息添加到 ModelState，ModelState 将返回值 false。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-249">If either property is missing a value, then a validation error message is added to ModelState and ModelState.IsValid returns the value false.</span></span>

<span data-ttu-id="9f5f9-250">最后，如果没有验证错误，则通过调用 SaveChanges （）方法，使用任何更改更新基础电影数据库表。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-250">Finally, if there are no validation errors, then the underlying Movies database table is updated with any changes by calling the SaveChanges() method.</span></span>

<span data-ttu-id="9f5f9-251">编辑数据库记录时，需要将正在编辑的记录的 Id 传递给执行数据库更新的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-251">When editing database records, you need to pass the Id of the record being edited to the controller action that performs the database update.</span></span> <span data-ttu-id="9f5f9-252">否则，控制器操作将不知道要在基础数据库中更新哪个记录。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-252">Otherwise, the controller action will not know which record to update in the underlying database.</span></span> <span data-ttu-id="9f5f9-253">"列表 5" 中包含的 "编辑" 视图包含一个隐藏的窗体字段，该字段表示正在编辑的数据库记录的 Id。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-253">The Edit view, contained in Listing 5, includes a hidden form field that represents the Id of the database record being edited.</span></span>

<span data-ttu-id="9f5f9-254">**列表5– Views\Home\Edit.aspx**</span><span class="sxs-lookup"><span data-stu-id="9f5f9-254">**Listing 5 – Views\Home\Edit.aspx**</span></span>

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample8.aspx)]

## <a name="deleting-database-records-with-the-entity-framework"></a><span data-ttu-id="9f5f9-255">删除具有实体框架的数据库记录</span><span class="sxs-lookup"><span data-stu-id="9f5f9-255">Deleting Database Records with the Entity Framework</span></span>

<span data-ttu-id="9f5f9-256">在本教程中，需要处理的最终数据库操作是删除数据库记录。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-256">The final database operation, which we need to tackle in this tutorial, is deleting database records.</span></span> <span data-ttu-id="9f5f9-257">您可以使用清单6中的控制器操作删除特定的数据库记录。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-257">You can use the controller action in Listing 6 to delete a particular database record.</span></span>

<span data-ttu-id="9f5f9-258">**列表 6--\Controllers\HomeController.cs （删除操作）**</span><span class="sxs-lookup"><span data-stu-id="9f5f9-258">**Listing 6 -- \Controllers\HomeController.cs (Delete action)**</span></span>

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample9.cs)]

<span data-ttu-id="9f5f9-259">Delete （）操作首先检索与传递给操作的 Id 相匹配的 "电影" 实体。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-259">The Delete() action first retrieves the Movie entity that matches the Id passed to the action.</span></span> <span data-ttu-id="9f5f9-260">接下来，通过调用 DeleteObject （）方法并随后使用 SaveChanges （）方法从数据库中删除此电影。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-260">Next, the movie is deleted from the database by calling the DeleteObject() method followed by the SaveChanges() method.</span></span> <span data-ttu-id="9f5f9-261">最后，将用户重定向回索引视图。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-261">Finally, the user is redirected back to the Index view.</span></span>

## <a name="summary"></a><span data-ttu-id="9f5f9-262">摘要</span><span class="sxs-lookup"><span data-stu-id="9f5f9-262">Summary</span></span>

<span data-ttu-id="9f5f9-263">本教程的目的是演示如何通过利用 ASP.NET MVC 和 Microsoft 实体框架来构建数据库驱动的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-263">The purpose of this tutorial was to demonstrate how you can build database-driven web applications by taking advantage of ASP.NET MVC and the Microsoft Entity Framework.</span></span> <span data-ttu-id="9f5f9-264">您学习了如何构建可用于选择、插入、更新和删除数据库记录的应用程序。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-264">You learned how to build an application that enables you to select, insert, update, and delete database records.</span></span>

<span data-ttu-id="9f5f9-265">首先，我们讨论了如何使用实体数据模型向导在 Visual Studio 中生成实体数据模型。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-265">First, we discussed how you can use the Entity Data Model Wizard to generate an Entity Data Model from within Visual Studio.</span></span> <span data-ttu-id="9f5f9-266">接下来，您将了解如何使用 LINQ to Entities 从数据库表中检索一组数据库记录。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-266">Next, you learn how to use LINQ to Entities to retrieve a set of database records from a database table.</span></span> <span data-ttu-id="9f5f9-267">最后，我们使用了实体框架来插入、更新和删除数据库记录。</span><span class="sxs-lookup"><span data-stu-id="9f5f9-267">Finally, we used the Entity Framework to insert, update, and delete database records.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="9f5f9-268">下一部分</span><span class="sxs-lookup"><span data-stu-id="9f5f9-268">Next</span></span>](creating-model-classes-with-linq-to-sql-cs.md)
