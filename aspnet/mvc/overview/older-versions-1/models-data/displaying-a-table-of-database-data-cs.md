---
uid: mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-cs
title: 显示数据库数据表（C#） |Microsoft Docs
author: microsoft
description: 在本教程中，我将演示显示一组数据库记录的两种方法。 我显示了两种在 HTML ta 中设置一组数据库记录格式的方法 。
ms.author: riande
ms.date: 10/07/2008
ms.assetid: d6e758b6-6571-484d-a132-34ee6c47747a
msc.legacyurl: /mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-cs
msc.type: authoredcontent
ms.openlocfilehash: 3c908d030076fc8400190ef3cf1672632ac1ed6b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74589456"
---
# <a name="displaying-a-table-of-database-data-c"></a><span data-ttu-id="8b02b-104">显示数据库数据表 (C#)</span><span class="sxs-lookup"><span data-stu-id="8b02b-104">Displaying a Table of Database Data (C#)</span></span>

<span data-ttu-id="8b02b-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="8b02b-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="8b02b-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="8b02b-106">Download PDF</span></span>](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_11_CS.pdf)

> <span data-ttu-id="8b02b-107">在本教程中，我将演示显示一组数据库记录的两种方法。</span><span class="sxs-lookup"><span data-stu-id="8b02b-107">In this tutorial, I demonstrate two methods of displaying a set of database records.</span></span> <span data-ttu-id="8b02b-108">我显示了两种用于对 HTML 表中的一组数据库记录进行格式设置的方法。</span><span class="sxs-lookup"><span data-stu-id="8b02b-108">I show two methods of formatting a set of database records in an HTML table.</span></span> <span data-ttu-id="8b02b-109">首先，我将介绍如何在视图中直接设置数据库记录的格式。</span><span class="sxs-lookup"><span data-stu-id="8b02b-109">First, I show how you can format the database records directly within a view.</span></span> <span data-ttu-id="8b02b-110">接下来，我将演示如何在设置数据库记录的格式时利用分区。</span><span class="sxs-lookup"><span data-stu-id="8b02b-110">Next, I demonstrate how you can take advantage of partials when formatting database records.</span></span>

<span data-ttu-id="8b02b-111">本教程的目的是介绍如何在 ASP.NET MVC 应用程序中显示数据库数据的 HTML 表。</span><span class="sxs-lookup"><span data-stu-id="8b02b-111">The goal of this tutorial is to explain how you can display an HTML table of database data in an ASP.NET MVC application.</span></span> <span data-ttu-id="8b02b-112">首先，您将了解如何使用 Visual Studio 中包含的基架工具来生成自动显示一组记录的视图。</span><span class="sxs-lookup"><span data-stu-id="8b02b-112">First, you learn how to use the scaffolding tools included in Visual Studio to generate a view that displays a set of records automatically.</span></span> <span data-ttu-id="8b02b-113">接下来，您将了解如何在设置数据库记录格式时使用部分作为模板。</span><span class="sxs-lookup"><span data-stu-id="8b02b-113">Next, you learn how to use a partial as a template when formatting database records.</span></span>

## <a name="create-the-model-classes"></a><span data-ttu-id="8b02b-114">创建模型类</span><span class="sxs-lookup"><span data-stu-id="8b02b-114">Create the Model Classes</span></span>

<span data-ttu-id="8b02b-115">我们将显示电影数据库表中的记录集。</span><span class="sxs-lookup"><span data-stu-id="8b02b-115">We are going to display the set of records from the Movies database table.</span></span> <span data-ttu-id="8b02b-116">电影数据库表包含以下列：</span><span class="sxs-lookup"><span data-stu-id="8b02b-116">The Movies database table contains the following columns:</span></span>

<a id="0.3_table01"></a>

| <span data-ttu-id="8b02b-117">**列名**</span><span class="sxs-lookup"><span data-stu-id="8b02b-117">**Column Name**</span></span> | <span data-ttu-id="8b02b-118">**数据类型**</span><span class="sxs-lookup"><span data-stu-id="8b02b-118">**Data Type**</span></span> | <span data-ttu-id="8b02b-119">**允许空值**</span><span class="sxs-lookup"><span data-stu-id="8b02b-119">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b02b-120">Id</span><span class="sxs-lookup"><span data-stu-id="8b02b-120">Id</span></span> | <span data-ttu-id="8b02b-121">Int</span><span class="sxs-lookup"><span data-stu-id="8b02b-121">Int</span></span> | <span data-ttu-id="8b02b-122">False</span><span class="sxs-lookup"><span data-stu-id="8b02b-122">False</span></span> |
| <span data-ttu-id="8b02b-123">职务</span><span class="sxs-lookup"><span data-stu-id="8b02b-123">Title</span></span> | <span data-ttu-id="8b02b-124">Nvarchar （200）</span><span class="sxs-lookup"><span data-stu-id="8b02b-124">Nvarchar(200)</span></span> | <span data-ttu-id="8b02b-125">False</span><span class="sxs-lookup"><span data-stu-id="8b02b-125">False</span></span> |
| <span data-ttu-id="8b02b-126">9509</span><span class="sxs-lookup"><span data-stu-id="8b02b-126">Director</span></span> | <span data-ttu-id="8b02b-127">NVarchar （50）</span><span class="sxs-lookup"><span data-stu-id="8b02b-127">NVarchar(50)</span></span> | <span data-ttu-id="8b02b-128">False</span><span class="sxs-lookup"><span data-stu-id="8b02b-128">False</span></span> |
| <span data-ttu-id="8b02b-129">DateReleased</span><span class="sxs-lookup"><span data-stu-id="8b02b-129">DateReleased</span></span> | <span data-ttu-id="8b02b-130">DateTime</span><span class="sxs-lookup"><span data-stu-id="8b02b-130">DateTime</span></span> | <span data-ttu-id="8b02b-131">False</span><span class="sxs-lookup"><span data-stu-id="8b02b-131">False</span></span> |

<span data-ttu-id="8b02b-132">为了表示我们的 ASP.NET MVC 应用程序中的电影表，我们需要创建一个模型类。</span><span class="sxs-lookup"><span data-stu-id="8b02b-132">In order to represent the Movies table in our ASP.NET MVC application, we need to create a model class.</span></span> <span data-ttu-id="8b02b-133">在本教程中，我们将使用 Microsoft 实体框架来创建模型类。</span><span class="sxs-lookup"><span data-stu-id="8b02b-133">In this tutorial, we use the Microsoft Entity Framework to create our model classes.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="8b02b-134">在本教程中，我们将使用 Microsoft 实体框架。</span><span class="sxs-lookup"><span data-stu-id="8b02b-134">In this tutorial, we use the Microsoft Entity Framework.</span></span> <span data-ttu-id="8b02b-135">但是，请务必了解，你可以使用各种不同的技术与 ASP.NET MVC 应用程序中的数据库进行交互，包括 LINQ to SQL、NHibernate 或 ADO.NET。</span><span class="sxs-lookup"><span data-stu-id="8b02b-135">However, it is important to understand that you can use a variety of different technologies to interact with a database from an ASP.NET MVC application including LINQ to SQL, NHibernate, or ADO.NET.</span></span>

<span data-ttu-id="8b02b-136">请按照以下步骤启动实体数据模型向导：</span><span class="sxs-lookup"><span data-stu-id="8b02b-136">Follow these steps to launch the Entity Data Model Wizard:</span></span>

1. <span data-ttu-id="8b02b-137">右键单击 "解决方案资源管理器" 窗口中的 "模型" 文件夹，然后选择 "**添加"、"新建项**" 菜单。</span><span class="sxs-lookup"><span data-stu-id="8b02b-137">Right-click the Models folder in the Solution Explorer window and the select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="8b02b-138">选择 "**数据**" 类别，然后选择 " **ADO.NET 实体数据模型**" 模板。</span><span class="sxs-lookup"><span data-stu-id="8b02b-138">Select the **Data** category and select the **ADO.NET Entity Data Model** template.</span></span>
3. <span data-ttu-id="8b02b-139">为数据模型指定名称*MoviesDBModel* ，并单击 "**添加**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="8b02b-139">Give your data model the name *MoviesDBModel.edmx* and click the **Add** button.</span></span>

<span data-ttu-id="8b02b-140">单击 "添加" 按钮后，将显示 "实体数据模型" 向导（参见图1）。</span><span class="sxs-lookup"><span data-stu-id="8b02b-140">After you click the Add button, the Entity Data Model Wizard appears (see Figure 1).</span></span> <span data-ttu-id="8b02b-141">按照以下步骤完成向导：</span><span class="sxs-lookup"><span data-stu-id="8b02b-141">Follow these steps to complete the wizard:</span></span>

1. <span data-ttu-id="8b02b-142">在 "**选择模型内容**" 步骤中，选择 "**从数据库生成**" 选项。</span><span class="sxs-lookup"><span data-stu-id="8b02b-142">In the **Choose Model Contents** step, select the **Generate from database** option.</span></span>
2. <span data-ttu-id="8b02b-143">在 "**选择你的数据连接**" 步骤中，使用*MoviesDB*数据连接，并为连接设置使用名称 " *MoviesDBEntities* "。</span><span class="sxs-lookup"><span data-stu-id="8b02b-143">In the **Choose Your Data Connection** step, use the *MoviesDB.mdf* data connection and the name *MoviesDBEntities* for the connection settings.</span></span> <span data-ttu-id="8b02b-144">单击 "**下一步**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="8b02b-144">Click the **Next** button.</span></span>
3. <span data-ttu-id="8b02b-145">在 "**选择数据库对象**" 步骤中，展开 "表" 节点，然后选择 "电影" 表。</span><span class="sxs-lookup"><span data-stu-id="8b02b-145">In the **Choose Your Database Objects** step, expand the Tables node, select the Movies table.</span></span> <span data-ttu-id="8b02b-146">输入命名空间*模型*，然后单击 "**完成**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="8b02b-146">Enter the namespace *Models* and click the **Finish** button.</span></span>

<span data-ttu-id="8b02b-147">[![创建 LINQ to SQL 类](displaying-a-table-of-database-data-cs/_static/image1.jpg)](displaying-a-table-of-database-data-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="8b02b-147">[![Creating LINQ to SQL classes](displaying-a-table-of-database-data-cs/_static/image1.jpg)](displaying-a-table-of-database-data-cs/_static/image1.png)</span></span>

<span data-ttu-id="8b02b-148">**图 01**：创建 LINQ to SQL 类（[单击以查看完全大小的图像](displaying-a-table-of-database-data-cs/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="8b02b-148">**Figure 01**: Creating LINQ to SQL classes ([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image2.png))</span></span>

<span data-ttu-id="8b02b-149">完成实体数据模型向导后，"实体数据模型设计器会打开。</span><span class="sxs-lookup"><span data-stu-id="8b02b-149">After you complete the Entity Data Model Wizard, the Entity Data Model Designer opens.</span></span> <span data-ttu-id="8b02b-150">设计器应显示电影实体（参见图2）。</span><span class="sxs-lookup"><span data-stu-id="8b02b-150">The Designer should display the Movies entity (see Figure 2).</span></span>

<span data-ttu-id="8b02b-151">[![实体数据模型设计器](displaying-a-table-of-database-data-cs/_static/image2.jpg)](displaying-a-table-of-database-data-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="8b02b-151">[![The Entity Data Model Designer](displaying-a-table-of-database-data-cs/_static/image2.jpg)](displaying-a-table-of-database-data-cs/_static/image3.png)</span></span>

<span data-ttu-id="8b02b-152">**图 02**：实体数据模型设计器（[单击查看完全大小的图像](displaying-a-table-of-database-data-cs/_static/image4.png)）</span><span class="sxs-lookup"><span data-stu-id="8b02b-152">**Figure 02**: The Entity Data Model Designer ([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image4.png))</span></span>

<span data-ttu-id="8b02b-153">在继续操作之前，我们需要进行一项更改。</span><span class="sxs-lookup"><span data-stu-id="8b02b-153">We need to make one change before we continue.</span></span> <span data-ttu-id="8b02b-154">实体数据向导将生成一个名为*电影*的模型类，该类表示电影数据库表。</span><span class="sxs-lookup"><span data-stu-id="8b02b-154">The Entity Data Wizard generates a model class named *Movies* that represents the Movies database table.</span></span> <span data-ttu-id="8b02b-155">由于我们将使用 movie 类来表示特定电影，因此我们需要将类的名称修改为*电影*，而不是*影片*（单数形式）。</span><span class="sxs-lookup"><span data-stu-id="8b02b-155">Because we'll use the Movies class to represent a particular movie, we need to modify the name of the class to be *Movie* instead of *Movies* (singular rather than plural).</span></span>

<span data-ttu-id="8b02b-156">双击设计器图面上类的名称，并将类的名称从 "电影" 更改为 "电影"。</span><span class="sxs-lookup"><span data-stu-id="8b02b-156">Double-click the name of the class on the designer surface and change the name of the class from Movies to Movie.</span></span> <span data-ttu-id="8b02b-157">做出此更改后，单击 "**保存**" 按钮（软盘的图标）以生成 Movie 类。</span><span class="sxs-lookup"><span data-stu-id="8b02b-157">After making this change, click the **Save** button (the icon of the floppy disk) to generate the Movie class.</span></span>

## <a name="create-the-movies-controller"></a><span data-ttu-id="8b02b-158">创建影片控制器</span><span class="sxs-lookup"><span data-stu-id="8b02b-158">Create the Movies Controller</span></span>

<span data-ttu-id="8b02b-159">现在我们有了表示数据库记录的方法，我们可以创建一个返回电影集合的控制器。</span><span class="sxs-lookup"><span data-stu-id="8b02b-159">Now that we have a way to represent our database records, we can create a controller that returns the collection of movies.</span></span> <span data-ttu-id="8b02b-160">在 Visual Studio 解决方案资源管理器 "窗口中，右键单击" 控制器 "文件夹，然后选择"**添加 "** 和" 控制器 "菜单选项（见图3）。</span><span class="sxs-lookup"><span data-stu-id="8b02b-160">Within the Visual Studio Solution Explorer window, right-click the Controllers folder and select the menu option **Add, Controller** (see Figure 3).</span></span>

<span data-ttu-id="8b02b-161">[!["添加控制器" 菜单](displaying-a-table-of-database-data-cs/_static/image3.jpg)](displaying-a-table-of-database-data-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="8b02b-161">[![The Add Controller Menu](displaying-a-table-of-database-data-cs/_static/image3.jpg)](displaying-a-table-of-database-data-cs/_static/image5.png)</span></span>

<span data-ttu-id="8b02b-162">**图 03**： "添加控制器" 菜单（[单击以查看完全大小的图像](displaying-a-table-of-database-data-cs/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="8b02b-162">**Figure 03**: The Add Controller Menu ([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image6.png))</span></span>

<span data-ttu-id="8b02b-163">"**添加控制器**" 对话框出现时，请输入控制器名称 MovieController （参见图4）。</span><span class="sxs-lookup"><span data-stu-id="8b02b-163">When the **Add Controller** dialog appears, enter the controller name MovieController (see Figure 4).</span></span> <span data-ttu-id="8b02b-164">单击 "**添加**" 按钮添加新控制器。</span><span class="sxs-lookup"><span data-stu-id="8b02b-164">Click the **Add** button to add the new controller.</span></span>

<span data-ttu-id="8b02b-165">[!["添加控制器" 对话框](displaying-a-table-of-database-data-cs/_static/image4.jpg)](displaying-a-table-of-database-data-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="8b02b-165">[![The Add Controller dialog](displaying-a-table-of-database-data-cs/_static/image4.jpg)](displaying-a-table-of-database-data-cs/_static/image7.png)</span></span>

<span data-ttu-id="8b02b-166">**图 04**： "添加控制器" 对话框（[单击以查看完全大小的映像](displaying-a-table-of-database-data-cs/_static/image8.png)）</span><span class="sxs-lookup"><span data-stu-id="8b02b-166">**Figure 04**: The Add Controller dialog([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image8.png))</span></span>

<span data-ttu-id="8b02b-167">我们需要修改电影控制器公开的 Index （）操作，使其返回一组数据库记录。</span><span class="sxs-lookup"><span data-stu-id="8b02b-167">We need to modify the Index() action exposed by the Movie controller so that it returns the set of database records.</span></span> <span data-ttu-id="8b02b-168">修改控制器，使其看起来像列表1中的控制器。</span><span class="sxs-lookup"><span data-stu-id="8b02b-168">Modify the controller so that it looks like the controller in Listing 1.</span></span>

<span data-ttu-id="8b02b-169">**列表1– Controllers\MovieController.cs**</span><span class="sxs-lookup"><span data-stu-id="8b02b-169">**Listing 1 – Controllers\MovieController.cs**</span></span>

[!code-csharp[Main](displaying-a-table-of-database-data-cs/samples/sample1.cs)]

<span data-ttu-id="8b02b-170">在列表1中，MoviesDBEntities 类用于表示 MoviesDB 数据库。</span><span class="sxs-lookup"><span data-stu-id="8b02b-170">In Listing 1, the MoviesDBEntities class is used to represent the MoviesDB database.</span></span> <span data-ttu-id="8b02b-171">若要使用此类，需导入 MvcApplication1 命名空间，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8b02b-171">To use this class, you need to import the MvcApplication1.Models namespace like this:</span></span>

<span data-ttu-id="8b02b-172">使用 MvcApplication1;</span><span class="sxs-lookup"><span data-stu-id="8b02b-172">using MvcApplication1.Models;</span></span>

<span data-ttu-id="8b02b-173">表达式*实体。MovieSet. System.linq.enumerable.tolist （）* 从电影数据库表中返回所有电影集。</span><span class="sxs-lookup"><span data-stu-id="8b02b-173">The expression *entities.MovieSet.ToList()* returns the set of all movies from the Movies database table.</span></span>

## <a name="create-the-view"></a><span data-ttu-id="8b02b-174">创建视图</span><span class="sxs-lookup"><span data-stu-id="8b02b-174">Create the View</span></span>

<span data-ttu-id="8b02b-175">若要在 HTML 表中显示一组数据库记录，最简单的方法是利用 Visual Studio 提供的基架。</span><span class="sxs-lookup"><span data-stu-id="8b02b-175">The easiest way to display a set of database records in an HTML table is to take advantage of the scaffolding provided by Visual Studio.</span></span>

<span data-ttu-id="8b02b-176">通过选择 "**生成、生成解决方案**" 菜单选项来生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="8b02b-176">Build your application by selecting the menu option **Build, Build Solution**.</span></span> <span data-ttu-id="8b02b-177">您必须先生成应用程序，然后才能打开 "**添加视图**" 对话框，否则您的数据类将不会出现在对话框中。</span><span class="sxs-lookup"><span data-stu-id="8b02b-177">You must build your application before opening the **Add View** dialog or your data classes won't appear in the dialog.</span></span>

<span data-ttu-id="8b02b-178">右键单击 Index （）操作并选择 "**添加视图**" 菜单选项（见图5）。</span><span class="sxs-lookup"><span data-stu-id="8b02b-178">Right-click the Index() action and select the menu option **Add View** (see Figure 5).</span></span>

<span data-ttu-id="8b02b-179">[添加视图 ![](displaying-a-table-of-database-data-cs/_static/image5.jpg)](displaying-a-table-of-database-data-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="8b02b-179">[![Adding a view](displaying-a-table-of-database-data-cs/_static/image5.jpg)](displaying-a-table-of-database-data-cs/_static/image9.png)</span></span>

<span data-ttu-id="8b02b-180">**图 05**：添加视图（[单击查看完全尺寸的图像](displaying-a-table-of-database-data-cs/_static/image10.png)）</span><span class="sxs-lookup"><span data-stu-id="8b02b-180">**Figure 05**: Adding a view ([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image10.png))</span></span>

<span data-ttu-id="8b02b-181">在 "**添加视图**" 对话框中，选中标记为 "**创建强类型视图**" 的复选框。</span><span class="sxs-lookup"><span data-stu-id="8b02b-181">In the **Add View** dialog, check the checkbox labeled **Create a strongly-typed view**.</span></span> <span data-ttu-id="8b02b-182">选择 Movie 类作为**视图数据类**。</span><span class="sxs-lookup"><span data-stu-id="8b02b-182">Select the Movie class as the **view data class**.</span></span> <span data-ttu-id="8b02b-183">选择 "*列表*" 作为 "**查看内容**" （见图6）。</span><span class="sxs-lookup"><span data-stu-id="8b02b-183">Select *List* as the **view content** (see Figure 6).</span></span> <span data-ttu-id="8b02b-184">选择这些选项将生成显示电影列表的强类型视图。</span><span class="sxs-lookup"><span data-stu-id="8b02b-184">Selecting these options will generate a strongly-typed view that displays a list of movies.</span></span>

<span data-ttu-id="8b02b-185">[!["添加视图" 对话框](displaying-a-table-of-database-data-cs/_static/image6.jpg)](displaying-a-table-of-database-data-cs/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="8b02b-185">[![The Add View dialog](displaying-a-table-of-database-data-cs/_static/image6.jpg)](displaying-a-table-of-database-data-cs/_static/image11.png)</span></span>

<span data-ttu-id="8b02b-186">**图 06**： "添加视图" 对话框（[单击以查看完全大小的图像](displaying-a-table-of-database-data-cs/_static/image12.png)）</span><span class="sxs-lookup"><span data-stu-id="8b02b-186">**Figure 06**: The Add View dialog([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image12.png))</span></span>

<span data-ttu-id="8b02b-187">单击 "**添加**" 按钮后，会自动生成列表2中的视图。</span><span class="sxs-lookup"><span data-stu-id="8b02b-187">After you click the **Add** button, the view in Listing 2 is generated automatically.</span></span> <span data-ttu-id="8b02b-188">此视图包含遍历电影集合并显示电影的每个属性所需的代码。</span><span class="sxs-lookup"><span data-stu-id="8b02b-188">This view contains the code required to iterate through the collection of movies and display each of the properties of a movie.</span></span>

<span data-ttu-id="8b02b-189">**列表 2-Views\Movie\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="8b02b-189">**Listing 2 – Views\Movie\Index.aspx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample2.aspx)]

<span data-ttu-id="8b02b-190">您可以通过选择菜单选项 "**调试"、"启动调试"** （或按 F5 键）来运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="8b02b-190">You can run the application by selecting the menu option **Debug, Start Debugging** (or hitting the F5 key).</span></span> <span data-ttu-id="8b02b-191">运行应用程序会启动 Internet Explorer。</span><span class="sxs-lookup"><span data-stu-id="8b02b-191">Running the application launches Internet Explorer.</span></span> <span data-ttu-id="8b02b-192">如果导航到/Movie URL，则会看到图7中的页面。</span><span class="sxs-lookup"><span data-stu-id="8b02b-192">If you navigate to the /Movie URL then you'll see the page in Figure 7.</span></span>

<span data-ttu-id="8b02b-193">[![电影表](displaying-a-table-of-database-data-cs/_static/image7.jpg)](displaying-a-table-of-database-data-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="8b02b-193">[![A table of movies](displaying-a-table-of-database-data-cs/_static/image7.jpg)](displaying-a-table-of-database-data-cs/_static/image13.png)</span></span>

<span data-ttu-id="8b02b-194">**图 07**：电影表（[单击以查看完全大小的图像](displaying-a-table-of-database-data-cs/_static/image14.png)）</span><span class="sxs-lookup"><span data-stu-id="8b02b-194">**Figure 07**: A table of movies([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image14.png))</span></span>

<span data-ttu-id="8b02b-195">如果您不喜欢图7中数据库记录网格外观的任何内容，则可以直接修改索引视图。</span><span class="sxs-lookup"><span data-stu-id="8b02b-195">If you don't like anything about the appearance of the grid of database records in Figure 7 then you can simply modify the Index view.</span></span> <span data-ttu-id="8b02b-196">例如，可以通过修改 "索引" 视图将*DateReleased*标头更改为 "已*发布*"。</span><span class="sxs-lookup"><span data-stu-id="8b02b-196">For example, you can change the *DateReleased* header to *Date Released* by modifying the Index view.</span></span>

## <a name="create-a-template-with-a-partial"></a><span data-ttu-id="8b02b-197">创建部分为的模板</span><span class="sxs-lookup"><span data-stu-id="8b02b-197">Create a Template with a Partial</span></span>

<span data-ttu-id="8b02b-198">视图变得过于复杂时，最好开始将视图分解为分区。</span><span class="sxs-lookup"><span data-stu-id="8b02b-198">When a view gets too complicated, it is a good idea to start breaking the view into partials.</span></span> <span data-ttu-id="8b02b-199">使用分区可使你的视图更易于理解和维护。</span><span class="sxs-lookup"><span data-stu-id="8b02b-199">Using partials makes your views easier to understand and maintain.</span></span> <span data-ttu-id="8b02b-200">我们将创建一个部分，可将其用作模板来设置每个电影数据库记录的格式。</span><span class="sxs-lookup"><span data-stu-id="8b02b-200">We'll create a partial that we can use as a template to format each of the movie database records.</span></span>

<span data-ttu-id="8b02b-201">请按照以下步骤创建部分：</span><span class="sxs-lookup"><span data-stu-id="8b02b-201">Follow these steps to create the partial:</span></span>

1. <span data-ttu-id="8b02b-202">右键单击 Views\Movie 文件夹，然后选择 "**添加视图**" 菜单。</span><span class="sxs-lookup"><span data-stu-id="8b02b-202">Right-click the Views\Movie folder and select the menu option **Add View**.</span></span>
2. <span data-ttu-id="8b02b-203">选中标签为 "*创建分部视图（.ascx）* " 的复选框。</span><span class="sxs-lookup"><span data-stu-id="8b02b-203">Check the checkbox labeled *Create a partial view (.ascx)*.</span></span>
3. <span data-ttu-id="8b02b-204">将部分*MovieTemplate*命名为。</span><span class="sxs-lookup"><span data-stu-id="8b02b-204">Name the partial *MovieTemplate*.</span></span>
4. <span data-ttu-id="8b02b-205">选中标签为 "**创建强类型视图**" 的复选框。</span><span class="sxs-lookup"><span data-stu-id="8b02b-205">Check the checkbox labeled **Create a strongly-typed view**.</span></span>
5. <span data-ttu-id="8b02b-206">选择 "影片" 作为 "*视图数据类*"。</span><span class="sxs-lookup"><span data-stu-id="8b02b-206">Select Movie as the *view data class*.</span></span>
6. <span data-ttu-id="8b02b-207">选择 "空" 作为 "*视图内容*"。</span><span class="sxs-lookup"><span data-stu-id="8b02b-207">Select Empty as the *view content*.</span></span>
7. <span data-ttu-id="8b02b-208">单击 "**添加**" 按钮，将部分添加到您的项目中。</span><span class="sxs-lookup"><span data-stu-id="8b02b-208">Click the **Add** button to add the partial to your project.</span></span>

<span data-ttu-id="8b02b-209">完成这些步骤后，将 MovieTemplate 部分修改为类似于列表3的外观。</span><span class="sxs-lookup"><span data-stu-id="8b02b-209">After you complete these steps, modify the MovieTemplate partial to look like Listing 3.</span></span>

<span data-ttu-id="8b02b-210">**列表 3-Views\Movie\MovieTemplate.ascx**</span><span class="sxs-lookup"><span data-stu-id="8b02b-210">**Listing 3 – Views\Movie\MovieTemplate.ascx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample3.aspx)]

<span data-ttu-id="8b02b-211">列表3中的部分包含一个用于记录单行的模板。</span><span class="sxs-lookup"><span data-stu-id="8b02b-211">The partial in Listing 3 contains a template for a single row of records.</span></span>

<span data-ttu-id="8b02b-212">列表4中修改的索引视图使用 MovieTemplate 部分。</span><span class="sxs-lookup"><span data-stu-id="8b02b-212">The modified Index view in Listing 4 uses the MovieTemplate partial.</span></span>

<span data-ttu-id="8b02b-213">**列表 4-Views\Movie\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="8b02b-213">**Listing 4 – Views\Movie\Index.aspx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample4.aspx)]

<span data-ttu-id="8b02b-214">列表4中的视图包含一个用于循环访问所有影片的 foreach 循环。</span><span class="sxs-lookup"><span data-stu-id="8b02b-214">The view in Listing 4 contains a foreach loop that iterates through all of the movies.</span></span> <span data-ttu-id="8b02b-215">对于每个电影，将使用 MovieTemplate 部分来设置电影的格式。</span><span class="sxs-lookup"><span data-stu-id="8b02b-215">For each movie, the MovieTemplate partial is used to format the movie.</span></span> <span data-ttu-id="8b02b-216">MovieTemplate 通过调用 RenderPartial （） helper 方法呈现。</span><span class="sxs-lookup"><span data-stu-id="8b02b-216">The MovieTemplate is rendered by calling the RenderPartial() helper method.</span></span>

<span data-ttu-id="8b02b-217">修改后的 "索引" 视图呈现数据库记录的完全相同的 HTML 表。</span><span class="sxs-lookup"><span data-stu-id="8b02b-217">The modified Index view renders the very same HTML table of database records.</span></span> <span data-ttu-id="8b02b-218">不过，视图已大大简化。</span><span class="sxs-lookup"><span data-stu-id="8b02b-218">However, the view has been greatly simplified.</span></span>

<span data-ttu-id="8b02b-219">RenderPartial （）方法不同于大多数其他 helper 方法，因为它不返回字符串。</span><span class="sxs-lookup"><span data-stu-id="8b02b-219">The RenderPartial() method is different than most of the other helper methods because it does not return a string.</span></span> <span data-ttu-id="8b02b-220">因此，必须使用 &lt;% RenderPartial （）调用 RenderPartial （）方法;%&gt; 而不是 &lt;% = RenderPartial （）;%&gt;。</span><span class="sxs-lookup"><span data-stu-id="8b02b-220">Therefore, you must call the RenderPartial() method using &lt;% Html.RenderPartial(); %&gt; instead of &lt;%= Html.RenderPartial(); %&gt;.</span></span>

## <a name="summary"></a><span data-ttu-id="8b02b-221">总结</span><span class="sxs-lookup"><span data-stu-id="8b02b-221">Summary</span></span>

<span data-ttu-id="8b02b-222">本教程的目的是说明如何在 HTML 表中显示一组数据库记录。</span><span class="sxs-lookup"><span data-stu-id="8b02b-222">The goal of this tutorial was to explain how you can display a set of database records in an HTML table.</span></span> <span data-ttu-id="8b02b-223">首先，您学习了如何通过利用 Microsoft 实体框架从控制器操作返回一组数据库记录。</span><span class="sxs-lookup"><span data-stu-id="8b02b-223">First, you learned how to return a set of database records from a controller action by taking advantage of the Microsoft Entity Framework.</span></span> <span data-ttu-id="8b02b-224">接下来，您学习了如何使用 Visual Studio 基架生成一个视图，该视图自动显示项的集合。</span><span class="sxs-lookup"><span data-stu-id="8b02b-224">Next, you learned how to use Visual Studio scaffolding to generate a view that displays a collection of items automatically.</span></span> <span data-ttu-id="8b02b-225">最后，您学习了如何通过利用部分来简化视图。</span><span class="sxs-lookup"><span data-stu-id="8b02b-225">Finally, you learned how to simplify the view by taking advantage of a partial.</span></span> <span data-ttu-id="8b02b-226">您已经学习了如何使用部分模板作为模板，以便您可以对每个数据库记录进行格式设置。</span><span class="sxs-lookup"><span data-stu-id="8b02b-226">You learned how to use a partial as a template so that you can format each database record.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8b02b-227">[上一页](creating-model-classes-with-linq-to-sql-cs.md)
> [下一页](performing-simple-validation-cs.md)</span><span class="sxs-lookup"><span data-stu-id="8b02b-227">[Previous](creating-model-classes-with-linq-to-sql-cs.md)
[Next](performing-simple-validation-cs.md)</span></span>
