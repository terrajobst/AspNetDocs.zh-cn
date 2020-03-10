---
uid: mvc/overview/getting-started/database-first-development/changing-the-database
title: 教程：通过 ASP.NET MVC 应用更改 EF Database First 数据库
description: 本教程重点介绍如何更新数据库结构并在整个 web 应用程序中传播该更改。
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: cfd5c083-a319-482e-8f25-5b38caa93954
msc.legacyurl: /mvc/overview/getting-started/database-first-development/changing-the-database
msc.type: authoredcontent
ms.openlocfilehash: 52cad1120908cf0d4f85770f8e2690f9415c5f56
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499520"
---
# <a name="tutorial-change-the-database-for-ef-database-first-with-aspnet-mvc-app"></a><span data-ttu-id="0e2e0-103">教程：通过 ASP.NET MVC 应用更改 EF Database First 数据库</span><span class="sxs-lookup"><span data-stu-id="0e2e0-103">Tutorial: Change the database for EF Database First with ASP.NET MVC app</span></span>

<span data-ttu-id="0e2e0-104">使用 MVC、实体框架和 ASP.NET 基架，你可以创建一个 web 应用程序，用于向现有数据库提供接口。</span><span class="sxs-lookup"><span data-stu-id="0e2e0-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="0e2e0-105">本系列教程演示如何自动生成允许用户显示、编辑、创建和删除位于数据库表中的数据的代码。</span><span class="sxs-lookup"><span data-stu-id="0e2e0-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="0e2e0-106">生成的代码与数据库表中的列相对应。</span><span class="sxs-lookup"><span data-stu-id="0e2e0-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="0e2e0-107">本教程重点介绍如何更新数据库结构并在整个 web 应用程序中传播该更改。</span><span class="sxs-lookup"><span data-stu-id="0e2e0-107">This tutorial focuses on making an update to the database structure and propagating that change throughout the web application.</span></span>

<span data-ttu-id="0e2e0-108">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="0e2e0-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0e2e0-109">添加列</span><span class="sxs-lookup"><span data-stu-id="0e2e0-109">Add a column</span></span>
> * <span data-ttu-id="0e2e0-110">将属性添加到视图</span><span class="sxs-lookup"><span data-stu-id="0e2e0-110">Add the property to the views</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e2e0-111">系统必备</span><span class="sxs-lookup"><span data-stu-id="0e2e0-111">Prerequisites</span></span>

* [<span data-ttu-id="0e2e0-112">正在生成视图</span><span class="sxs-lookup"><span data-stu-id="0e2e0-112">Generating views</span></span>](generating-views.md)

## <a name="add-a-column"></a><span data-ttu-id="0e2e0-113">添加列</span><span class="sxs-lookup"><span data-stu-id="0e2e0-113">Add a column</span></span>

<span data-ttu-id="0e2e0-114">如果更新数据库中表的结构，则需要确保将更改传播到数据模型、视图和控制器。</span><span class="sxs-lookup"><span data-stu-id="0e2e0-114">If you update the structure of a table in your database, you need to ensure that your change is propagated to the data model, views, and controller.</span></span>

<span data-ttu-id="0e2e0-115">对于本教程，您将向 "学生" 表添加一个新列，以记录学生的中间名。</span><span class="sxs-lookup"><span data-stu-id="0e2e0-115">For this tutorial, you will add a new column to the Student table to record the middle name of the student.</span></span> <span data-ttu-id="0e2e0-116">若要添加此列，请打开数据库项目，然后打开 Student .sql 文件。</span><span class="sxs-lookup"><span data-stu-id="0e2e0-116">To add this column, open the database project, and open the Student.sql file.</span></span> <span data-ttu-id="0e2e0-117">通过设计器或 T-sql 代码，添加一个名为**MiddleName**的列，该列的数据类型为 NVARCHAR （50），并允许空值。</span><span class="sxs-lookup"><span data-stu-id="0e2e0-117">Through either the designer or the T-SQL code, add a column named **MiddleName** that is an NVARCHAR(50) and allows NULL values.</span></span>

<span data-ttu-id="0e2e0-118">通过启动您的数据库项目（或按 F5），将此更改部署到您的本地数据库。</span><span class="sxs-lookup"><span data-stu-id="0e2e0-118">Deploy this change to your local database by starting your database project (or F5).</span></span> <span data-ttu-id="0e2e0-119">新字段将添加到表中。</span><span class="sxs-lookup"><span data-stu-id="0e2e0-119">The new field is added to the table.</span></span> <span data-ttu-id="0e2e0-120">如果在 SQL Server 对象资源管理器中看不到它，请单击窗格中的 "刷新" 按钮。</span><span class="sxs-lookup"><span data-stu-id="0e2e0-120">If you do not see it in the SQL Server Object Explorer, click the Refresh button in the pane.</span></span>

![显示新列](changing-the-database/_static/image2.png)

<span data-ttu-id="0e2e0-122">新列存在于数据库表中，但它当前不存在于数据模型类中。</span><span class="sxs-lookup"><span data-stu-id="0e2e0-122">The new column exists in the database table, but it does not currently exist in the data model class.</span></span> <span data-ttu-id="0e2e0-123">您必须更新模型以包含您的新列。</span><span class="sxs-lookup"><span data-stu-id="0e2e0-123">You must update the model to include your new column.</span></span> <span data-ttu-id="0e2e0-124">在 "**模型**" 文件夹中，打开**ContosoModel**文件以显示模型关系图。</span><span class="sxs-lookup"><span data-stu-id="0e2e0-124">In the **Models** folder, open the **ContosoModel.edmx** file to display the model diagram.</span></span> <span data-ttu-id="0e2e0-125">请注意，"学生" 模型不包含 MiddleName 属性。</span><span class="sxs-lookup"><span data-stu-id="0e2e0-125">Notice that the Student model does not contain the MiddleName property.</span></span> <span data-ttu-id="0e2e0-126">右键单击设计图面上的任意位置，然后选择 "**从数据库更新模型**"。</span><span class="sxs-lookup"><span data-stu-id="0e2e0-126">Right-click anywhere on the design surface, and select **Update Model from Database**.</span></span>

<span data-ttu-id="0e2e0-127">在更新向导中，选择 "**刷新**" 选项卡，然后选择 "**表** > **dbo** > **Student**"。</span><span class="sxs-lookup"><span data-stu-id="0e2e0-127">In the Update Wizard, select the **Refresh** tab and then select **Tables** > **dbo** > **Student**.</span></span> <span data-ttu-id="0e2e0-128">单击“完成”。</span><span class="sxs-lookup"><span data-stu-id="0e2e0-128">Click **Finish**.</span></span>

<span data-ttu-id="0e2e0-129">更新过程完成后，数据库关系图将包含新的**MiddleName**属性。</span><span class="sxs-lookup"><span data-stu-id="0e2e0-129">After the update process is finished, the database diagram includes the new **MiddleName** property.</span></span> <span data-ttu-id="0e2e0-130">保存**ContosoModel**文件。</span><span class="sxs-lookup"><span data-stu-id="0e2e0-130">Save the **ContosoModel.edmx** file.</span></span> <span data-ttu-id="0e2e0-131">若要将新属性传播到**Student.cs**类，必须保存此文件。</span><span class="sxs-lookup"><span data-stu-id="0e2e0-131">You must save this file for the new property to be propagated to the **Student.cs** class.</span></span> <span data-ttu-id="0e2e0-132">现已更新数据库和模型。</span><span class="sxs-lookup"><span data-stu-id="0e2e0-132">You have now updated the database and the model.</span></span>

<span data-ttu-id="0e2e0-133">生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="0e2e0-133">Build the solution.</span></span>

## <a name="add-the-property-to-the-views"></a><span data-ttu-id="0e2e0-134">将属性添加到视图</span><span class="sxs-lookup"><span data-stu-id="0e2e0-134">Add the property to the views</span></span>

<span data-ttu-id="0e2e0-135">遗憾的是，视图仍不包含新属性。</span><span class="sxs-lookup"><span data-stu-id="0e2e0-135">Unfortunately, the views still do not contain the new property.</span></span> <span data-ttu-id="0e2e0-136">若要更新视图，可以使用两个选项来重新生成视图，方法是再次添加 Student 类的基架，也可以手动将新属性添加到现有视图。</span><span class="sxs-lookup"><span data-stu-id="0e2e0-136">To update the views you have two options - you can either re-generate the views by once again adding scaffolding for the Student class, or you can manually add the new property to your existing views.</span></span> <span data-ttu-id="0e2e0-137">在本教程中，您将再次添加基架，因为您没有对自动生成的视图进行任何自定义更改。</span><span class="sxs-lookup"><span data-stu-id="0e2e0-137">In this tutorial, you will add the scaffolding again because you have not made any customized changes to the automatically-generated views.</span></span> <span data-ttu-id="0e2e0-138">如果对视图进行了更改，并且不希望放弃这些更改，则可以考虑手动添加属性。</span><span class="sxs-lookup"><span data-stu-id="0e2e0-138">You might consider manually adding the property when you have made changes to the views and do not want to lose those changes.</span></span>

<span data-ttu-id="0e2e0-139">若要确保重新创建视图，请在 "**视图**" 下删除 "**学生**" 文件夹，并删除**StudentsController**。</span><span class="sxs-lookup"><span data-stu-id="0e2e0-139">To ensure the views are re-created, delete the **Students** folder under **Views**, and delete the **StudentsController**.</span></span> <span data-ttu-id="0e2e0-140">然后，右键单击 "**控制器**" 文件夹并添加 "**学生**" 模型的基架。</span><span class="sxs-lookup"><span data-stu-id="0e2e0-140">Then, right-click the **Controllers** folder and add scaffolding for the **Student** model.</span></span> <span data-ttu-id="0e2e0-141">同样，将控制器命名为**StudentsController**。</span><span class="sxs-lookup"><span data-stu-id="0e2e0-141">Again, name the controller **StudentsController**.</span></span> <span data-ttu-id="0e2e0-142">选择“添加”。</span><span class="sxs-lookup"><span data-stu-id="0e2e0-142">Select **Add**.</span></span>

<span data-ttu-id="0e2e0-143">再次生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="0e2e0-143">Build the solution again.</span></span> <span data-ttu-id="0e2e0-144">视图现在包含 MiddleName 属性。</span><span class="sxs-lookup"><span data-stu-id="0e2e0-144">The views now contain the MiddleName property.</span></span>

![显示中间名](changing-the-database/_static/image5.png)

## <a name="next-steps"></a><span data-ttu-id="0e2e0-146">后续步骤</span><span class="sxs-lookup"><span data-stu-id="0e2e0-146">Next steps</span></span>

<span data-ttu-id="0e2e0-147">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="0e2e0-147">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0e2e0-148">添加了列</span><span class="sxs-lookup"><span data-stu-id="0e2e0-148">Added a column</span></span>
> * <span data-ttu-id="0e2e0-149">向视图添加了属性</span><span class="sxs-lookup"><span data-stu-id="0e2e0-149">Added the property to the views</span></span>

<span data-ttu-id="0e2e0-150">转到下一教程，了解如何自定义视图以显示有关学生记录的详细信息。</span><span class="sxs-lookup"><span data-stu-id="0e2e0-150">Advance to the next tutorial to learn how to customize the view for showing details about a student record.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="0e2e0-151">自定义视图</span><span class="sxs-lookup"><span data-stu-id="0e2e0-151">Customize a view</span></span>](customizing-a-view.md)